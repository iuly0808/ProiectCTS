# ProiectCTS Test Case-uri
Proiect CTS Mugea Iuliana Florentina 1053

package ro.ase.csie.cts.test;

import ro.ase.csie.cts.AccountException;
import ro.ase.csie.cts.CNPWCharactersException;
import ro.ase.csie.cts.CreditNotZeroEx;
import ro.ase.csie.cts.FloatingValueException;
import ro.ase.csie.cts.InvalidAgeException;
import ro.ase.csie.cts.NegativeCreditException;
import ro.ase.csie.cts.NumeWNumbersEx;
import ro.ase.csie.cts.OrasLengthException;
import ro.ase.csie.cts.OrasWNumbersEx;
import ro.ase.csie.cts.PrenumeWNumbersEx;
import ro.ase.csie.cts.TooBigCreditException;
import ro.ase.csie.cts.WrongCNPBeginning;
import ro.ase.csie.cts.WrongCNPLength;
import ro.ase.csie.cts.WrongGenException;
import ro.ase.csie.cts.WrongGenLengthEx;
import ro.ase.csie.cts.WrongNumeCharactersEx;
import ro.ase.csie.cts.ZeroCreditException;
import ro.ase.csie.cts.WrongNumeCharactersEx;
import ro.ase.csie.cts.WrongPrenumeCharactersEx;
import ro.ase.csie.cts.WrongNumberException;
import ro.ase.csie.cts.NumberWCharactersException;
import ro.ase.csie.cts.WrongNStringException;
import ro.ase.csie.cts.WrongPStringException;
import ro.ase.csie.cts.WrongBeginning;
import ro.ase.csie.cts.PhoneCreditAcc;
import junit.framework.TestCase;


public class TestPhoneCreditAcc extends TestCase {

	PhoneCreditAcc account;
	
	public void setUp(){
		System.out.println("setUp Unit test");
		account = new PhoneCreditAcc("0749248044","Mugea","Iuliana",40,"2930808183309","F",21,"Bucuresti");
	}
	
	//unit test pentru verificat metoda Incarcare()
	  //testare valori normale (intregi, pozitive)
		public void testNormalValuesIncarcare() throws NegativeCreditException, ZeroCreditException, FloatingValueException, TooBigCreditException
		{	
			double expected = 80;
			account.Incarcare(40.0);
			assertEquals("Test Incarcare() cu valori normale",
					80.0,
					account.getCredit(),
					0.0);
		}
		

		//testare valori negative (< 0)
		public void testNegativeValuesIncarcare() throws NegativeCreditException{
			try{
			account.Incarcare(-50.0);
			assertFalse("Metoda nu arunca exceptie pe valori negative", true);
			}
			catch(AccountException ex){
				assertTrue(true);	}
		}
		
			
		//testare valori nule (= 0)
		public void testZeroValueIncarcare() throws  ZeroCreditException{
			try{
			account.Incarcare(0.0);
			assertFalse("Metoda Incarcare() nu arunca exceptie pe 0", true);
			}
			catch(AccountException ex){
				assertTrue(true);	}
		}
		
		
		//testare valori pozitive cu maxim 2 zecimale
		public void testFloatingValueIncarcare()throws FloatingValueException {
			try{
			account.Incarcare(0.0006);
			assertFalse("Metoda Incarcare() nu arunca exceptie pe 0", true);
			}
			catch(AccountException ex){
				assertTrue(true);
			}
		}
		
		//testare valori > 1000
		public void testTooBigValueIncarcare() throws TooBigCreditException{
			try{
			account.Incarcare(200000);
			assertFalse("Metoda Incarcare() nu arunca exceptie pe 0", true);
			}
			catch(AccountException ex){
				assertTrue(true);
			}
		}
	
	
	
    //unit test pentru verificat metoda ValidareNumar()
		//testare numar caractere in numarul de telefon (10)		
		public void testNumarCifreNumar() throws WrongNumberException{
			try{
				account.ValidareNumar("074924804498");
				assertFalse("Metoda ValidareNumar() nu arunca exceptie", true);
				}
				catch(AccountException ex){
					assertTrue(true);	}
			}
		
		//testare caractere in numarul de telefon (fara litere, caractere neobisnuite)		
		public void testLitereNumar() throws NumberWCharactersException{
			try{
				account.ValidareNumar("07A9248o4");
				assertFalse("Metoda ValidareNumar() nu arunca exceptie", true);
				}
				catch(AccountException ex){
					assertTrue(true);	}
			}
		
		//testare inceput numar de telefon (07...)		
		public void testInceputNumar() throws WrongBeginning{
			try{
				account.ValidareNumar("0849248045");
				assertFalse("Metoda ValidareNumar() nu arunca exceptie", true);
				}
				catch(AccountException ex){
					assertTrue(true);	}
			}
	
		
	//unit test pentru verificat metoda ValidareNume()
		//testare numar caractere in nume (>30)			
		public void testNormalValidareNume30() throws WrongNumeCharactersEx{
			try{
				account.ValidareNume("AbracadabraPopescuIonescuMarinescuStanLazar");
				assertFalse("Metoda ValidareNume() nu arunca exceptie", true);
				}
				catch(AccountException ex){
					assertTrue(true);	}
			}
		
		//testare numar caractere in nume (<2)
		public void testNormalValidareNume2() throws WrongNumeCharactersEx{
			try{
				account.ValidareNume("A");
				assertFalse("Metoda ValidareNume() nu arunca exceptie", true);
				}
				catch(AccountException ex){
					assertTrue(true);	}
			}
		
		//testare caractere neobisnuite in nume (#,@,$,*)
		public void testValidareNumeString() throws WrongNStringException{
			try{
			    account.ValidareNume("Pope$cu");
				assertFalse("Metoda ValidareNume() nu arunca exceptie", true);
				}
				catch(AccountException ex){
					assertTrue(true);	}
			}
		
		//testare cifre in nume 
		public void testCifreNume() throws NumeWNumbersEx{
			try{
			    account.ValidareNume("Pope5cu");
				assertFalse("Metoda ValidareNume() nu arunca exceptie", true);
				}
				catch(AccountException ex){
					assertTrue(true);	}
			}
		
		
	//unit test pentru verificat metoda ValidarePrenume()
		//testare numar caractere in nume (>30)		
		
		public void testNormalValidarePrenume30() throws WrongPrenumeCharactersEx{
			try{
				account.ValidarePrenume("AbracadabraAnaPaulaAlinaAndreeaIulianaFlorentina");
				assertFalse("Metoda ValidareNumar() nu arunca exceptie", true);
				}
				catch(AccountException ex){
					assertTrue(true);	}
			}
		
		//testare numar caractere in nume (<2)				
		public void testNormalValidarePrenume2() throws WrongPrenumeCharactersEx{
			try{
				account.ValidarePrenume("B");
				assertFalse("Metoda ValidarePrenume() nu arunca exceptie", true);
				}
				catch(AccountException ex){							
					assertTrue(true);	}
				}
		
		//testare caractere neobisnuite in prenume (#,@,$,*)
		public void testValidarePrenumeString() throws WrongPStringException{
			try{
			    account.ValidarePrenume("Iuli@na");						
			    assertFalse("Metoda ValidarePrenume() nu arunca exceptie", true);
				}
				catch(AccountException ex){
					assertTrue(true);	}
				}
		
		//testare cifre in prenume 
		public void testCifrePreume() throws PrenumeWNumbersEx{
			try{
			    account.ValidarePrenume("Iuli4n4");
				assertFalse("Metoda ValidarePrenume() nu arunca exceptie", true);
				}
				catch(AccountException ex){
					assertTrue(true);	}
			}
	
	
		
	//unit test pentru verificat metoda ValidareCNP()
			//testare numar caractere in CNP (13)		
			public void testNumarCaractereCNP() throws WrongCNPLength{
				try{
					account.ValidareCNP("29308085699025");
					assertFalse("Metoda ValidareCNP() nu arunca exceptie", true);
					}
					catch(AccountException ex){
						assertTrue(true);	}
				}
				
			//testare inceput CNP (1 sau 2)		
			public void testInceputCNP() throws WrongCNPBeginning{
				try{
					account.ValidareNumar("6930808179045");
					assertFalse("Metoda ValidareCNP() nu arunca exceptie", true);
					}
					catch(AccountException ex){
						assertTrue(true);	}
				}
				
			//testare litere in CNP (fara litere)		
			public void testLitereCNP() throws CNPWCharactersException{
				try{
					account.ValidareNumar("293o8081B9045");
					assertFalse("Metoda ValidareCNP() nu arunca exceptie", true);
					}
					catch(AccountException ex){
						assertTrue(true);	}
				}
			
			
	//unit test pentru verificat metoda ValidareGen()
			//testare lungime camp gen (1 caracter)		
			public void testLungimeGenValida() throws WrongGenLengthEx{
				try{
					account.ValidareGen("FEM");
					assertFalse("Metoda ValidareGen() nu arunca exceptie", true);
					}
					catch(AccountException ex){
						assertTrue(true);	}
				}
			
			//testare gen valid (F/M)		
			public void testGenValid() throws WrongGenException{
				try{
					account.ValidareGen("B");
					assertFalse("Metoda ValidareGen() nu arunca exceptie", true);
					}
					catch(AccountException ex){
						assertTrue(true);	}
				}
			
		
			
	//unit test pentru verificat metoda ValidareVarsta()
			//testare varsta (<99)		
			public void testVarstaNormala() throws InvalidAgeException{
				try{
					account.ValidareVarsta(100);
					assertFalse("Metoda ValidareVarsta() nu arunca exceptie", true);
					}
					catch(AccountException ex){
						assertTrue(true);	}
				}

			
	//unit test pentru verificat metoda ValidareOras()
			//testare numar caractere in nume (>4)				
			public void testLungimeValidareOras() throws OrasLengthException{
				try{
					account.ValidareOras("Li");
					assertFalse("Metoda ValidarOras() nu arunca exceptie", true);
					}
					catch(AccountException ex){
						assertTrue(true);	}
				}
			
			
			//testare cifre in oras (>= 4)					
			public void testCifreValidareOras() throws OrasWNumbersEx{
				try{
					account.ValidareOras("Ar4d");
					assertFalse("Metoda ValidarOras() nu arunca exceptie", true);
					}
					catch(AccountException ex){
						assertTrue(true);	}
				}
			
			
			
	//unit test pentru verificat metoda InchidereCont()
			//testare valoare credit (diferita de 0)
			public void testInchidereCont() throws CreditNotZeroEx{
				try{
					account.InchidereCont("0749248044",100);
					assertFalse("Metoda InchidereCont() nu arunca exceptie", true);
					}
					catch(AccountException ex){
						assertTrue(true);	}
				}
					
}


