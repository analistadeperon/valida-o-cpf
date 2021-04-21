# valida-o-cpf
/*
 * To change this license header, choose License Headers in Project Properties.
 * To change this template file, choose Tools | Templates
 * and open the template in the editor.
 */
package cadastro.pessoas;

import java.util.Random;

/**
 *
 * @author anali
 */
public class classeCPF {
    /**
    * Gera numero de CPF randomico.
    * @return Novo CPF
    * @see generateDigits(String digitsBase)
    */
    public String generate(){
 
        Random r = new Random();
 
        StringBuilder sbCpfNumber = new StringBuilder();
 
        for(int i = 0; i < 10; i++){
 
            sbCpfNumber.append(r.nextInt(10));
 
        }
 
        return generateDigits(sbCpfNumber.toString());
 
    }
 
    /**
    * Valida o CPF.
    * @param cpf Numero de CPF sem pontuacao.
    * @return true para CPF valido ou o contrario.
    */
    public boolean validateCPF(String cpf){
 
        if(cpf.length() == 11){
 
            if(cpf.equals(generateDigits(cpf.substring(0, 10)))){
 
                return true;
 
            }
 
        }
 
        return false;
 
    }
 
    /**
    * Gera digitos validadores.
    * @param digitsBase 9 digitos iniciais.
    * @return CPF com digitos validadores sem pontuacao.
    */
    private String generateDigits(String digitsBase) {
 
        StringBuilder sbCpfNumber = new StringBuilder(digitsBase);
 
        int total = 0;
 
        int multiple = digitsBase.length() + 1;
 
        for (char digit : digitsBase.toCharArray()) {
 
            long parcial = Integer.parseInt(String.valueOf(digit)) * (multiple--);
 
            total += parcial;
 
        }
 
        int resto = Integer.parseInt(String.valueOf(Math.abs(total % 11)));
 
        if (resto < 2) {
 
            resto = 0;
 
        } else {
 
            resto = 11 - resto;
 
        }
 
        sbCpfNumber.append(resto);
 
        if (sbCpfNumber.length() < 11) {
 
            return generateDigits(sbCpfNumber.toString());
 
        }
 
        return sbCpfNumber.toString();
 
    }
 
}

