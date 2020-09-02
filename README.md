# School game store
//The school game store --- a code developed in C++ ---- with a set of games and a score board 
//***************************************************************
//                   HEADER FILE USED IN PROJECT
//****************************************************************

#include<fstream.h>
#include<conio.h>
#include<stdio.h>
#include<process.h>
#include<string.h>
#include<iomanip.h>
#include<time.h>
#include<stdlib.h>
void board();
int checkwin();
void tic_tac_toe();
int letterFill(char,char[],char[]);
void draw_line(int,char);
void rules();
void gamescore(char[],char[],int,int);
void play_dice(int);
void draw_line1(int,char);
void board1();
//***************************************************************
//                   CLASS USED IN PROJECT
//****************************************************************
class student
{
	char admno[6];
	char name[20];
	char stbno[6];
	int gamen;
public:
   void adds(int x);
	void create_student()
	{
		clrscr();
	 	cout<<"\nNEW STUDENT ENTRY...\n";
		cout<<"\nEnter The admission id. ";
		cin>>admno;
      int c=check_sps(admno);
      if(c==1)
      cout<<"\n\nOh!This admission id already exists";
      else
		{cout<<"\n\nEnter The Name of The Student ";
		 gets(name);
		 gamen=0;
				cout<<"\n\nStudent Record Created.."; }
	}

   int check_sps(char n[])
{
   ifstream fp;
   student st;
   int flag=0;
	fp.open("stud.dat",ios::in);
	while(fp.read((char*)&st,sizeof(student)))
	{
		if((strcmpi(st.retadmno(),n)==0))
		{

        flag=1;
		}
	}
   return flag;
   }
	void show_student()
	{
		cout<<"\nAdmission id. : "<<admno;
		cout<<"\nStudent Name : ";
		puts(name);
		cout<<"\nScores won: "<<gamen;

	}

	void modify_student()
	{
		cout<<"\nAdmission id. : "<<admno;
		cout<<"\nModify Student Name : ";
		gets(name);
	}

	char* retadmno()
	{
		return admno;
	}

   int retgamen()
   {
     return gamen;
     }

void report()
	{cout<<"\t"<<admno<<setw(20)<<name<<setw(10)<<gamen<<endl;}
 };

 void student::adds(int x)
 {gamen+=x;
 }

 void score(int n, char m[ ])
{

	int amt;
	bool found=false;
	student ac;
	fstream File;
	File.open("stud.dat", ios::binary|ios::in|ios::out);
	if(!File)
	{
		cout<<"File could not be open !! Press any Key...";
		return;
	}
	while(!File.eof() && found==false)
	{
		File.read(reinterpret_cast<char *> (&ac), sizeof(student));
		if(strcmp(ac.retadmno( ),m)==0)

       {ac.adds(n);


         int pos=(-1)*static_cast<int>(sizeof(ac));
			File.seekp(pos,ios::cur);
			File.write(reinterpret_cast<char *> (&ac), sizeof(student));
			cout<<"\n\n\t Record Updated";
			found=true;
	       }
         }
	File.close();
	if(found==false)
		cout<<"\n\n Record Not Found ";}

char square[10]={'0','1','2','3','4','5','6','7','8','9'};

void tic_tac_toe()

{
   char n[6];
	int player = 1,i,choice;
	char mark;
	clrscr();
	do
	{
		board();
		player=(player%2)?1:2;
		cout << "Player " << player << ", enter a number:  ";
		cin >> choice;
		mark=(player == 1) ? 'X' : 'O';
		if (choice == 1 && square[1] == '1')
			square[1] = mark;
		else if (choice == 2 && square[2] == '2')
			square[2] = mark;
		else if (choice == 3 && square[3] == '3')
			square[3] = mark;
		else if (choice == 4 && square[4] == '4')
			square[4] = mark;
		else if (choice == 5 && square[5] == '5')
			square[5] = mark;
		else if (choice == 6 && square[6] == '6')
			square[6] = mark;
		else if (choice == 7 && square[7] == '7')
			square[7] = mark;
		else if (choice == 8 && square[8] == '8')
			square[8] = mark;
		else if (choice == 9 && square[9] == '9')
			square[9] = mark;
		else
		{
			cout<<"Invalid move ";
			player--;
			getch();
		}
		i=checkwin();
		player++;
	}while(i==-1);
	board();
	if(i==1)
	{
		cout<<"==>\aPlayer "<<--player<<" win ";
cout<<"give the admission id of the winner";

cin>>n;//////////////////////
score(5,n);
} /////////////////////////
	else
		cout<<"==>\aGame draw";
	getch();
	}
	//return 0;

/*********************************************
	FUNCTION TO RETURN GAME STATUS
	1 FOR GAME IS OVER WITH RESULT
	-1 FOR GAME IS IN PROGRESS
	O GAME IS OVER AND NO RESULT
**********************************************/

int checkwin()
{
	if (square[1] == square[2] && square[2] == square[3])
		return 1;
	else if (square[4] == square[5] && square[5] == square[6])
		return 1;
	else if (square[7] == square[8] && square[8] == square[9])
		return 1;
	else if (square[1] == square[4] && square[4] == square[7])
		return 1;
	else if (square[2] == square[5] && square[5] == square[8])
		return 1;
	else if (square[3] == square[6] && square[6] == square[9])
		return 1;
	else if (square[1] == square[5] && square[5] == square[9])
		return 1;
	else if (square[3] == square[5] && square[5] == square[7])
		return 1;
	else if (square[1] != '1' && square[2] != '2' && square[3] != '3' &&
	         square[4] != '4' && square[5] != '5' && square[6] != '6' &&
            square[7] != '7' && square[8] != '8' && square[9] != '9')
		return 0;
	else
		return -1;
}


/*******************************************************************
     FUNCTION TO DRAW BOARD OF TIC TAC TOE WITH PLAYERS MARK
********************************************************************/


void board()
{
	clrscr();
	cout << "\n\n\tTic Tac Toe\n\n";
	cout << "Player 1 (X)  -  Player 2 (O)" << endl << endl;
	cout << endl;
	cout << "     |     |     " << endl;
	cout << "  " << square[1] << "  |  " << square[2] << "  |  " << square[3] << endl;
	cout << "_____|_____|_____" << endl;
	cout << "     |     |     " << endl;
	cout << "  " << square[4] << "  |  " << square[5] << "  |  " << square[6] << endl;
	cout << "_____|_____|_____" << endl;
	cout << "     |     |     " << endl;
	cout << "  " << square[7] << "  |  " << square[8] << "  |  " << square[9] << endl;
	cout << "     |     |     " << endl << endl;
}
  //} //////////////////////////////////
//*****************************************************************
//				END OF PROJECT
//*****************************************************************
//} ////////////////////////




 const int MAXLENGTH=80;
const int MAX_TRIES=5;
const int MAXROW=7;



void Hang_man()
{  char m[6];
	char unknown [MAXLENGTH];
	char letter;
	int num_of_wrong_guesses=0;
	char word[MAXLENGTH];
	char words[][MAXLENGTH] =
	{
		"india",
		"pakistan",
		"nepal",
		"malaysia",
		"philippines",
		"australia",
		"iran",
		"ethiopia",
		"oman",
		"indonesia"
	};

	//choose and copy a word from array of words randomly
	randomize();
	int n=random(10);
	strcpy(word,words[n]);

	// Initialize the secret word with the * character.


	int i;
	int length = strlen(word);
	for (i = 0; i < length; i++)
		unknown[i]='*';
	unknown[i]='\0';


		// welcome the user
	cout << "\n\nWelcome to hangman...Guess a country Name";
	cout << "\n\nEach letter is represented by a star.";
	cout << "\n\nYou have to type only one letter in one try";
	cout << "\n\nYou have " << MAX_TRIES << " tries to try and guess the word.";
	cout << "\n~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~";
   cout<<"\n\n\nEnter your admission id";
   cin>>m;

	// Loop until the guesses are used up
	while (num_of_wrong_guesses < MAX_TRIES)
	{
		cout << "\n\n" << unknown;
		cout << "\n\nGuess a letter: ";
		cin >> letter;
		// Fill secret word with letter if the guess is correct,
		// otherwise increment the number of wrong guesses.
		if (letterFill(letter, word, unknown)==0)
		{
			cout << endl << "\nWhoops! That letter isn't in there!" << endl;
			num_of_wrong_guesses++;
          score(-1,m);
		}
		else
		{
			cout << endl <<"\nYou found a letter! Isn't that exciting!" << endl;
         score(3,m);
		}
		// Tell user how many guesses has left.
		cout << "\nYou have " << MAX_TRIES - num_of_wrong_guesses;
		cout << " \nguesses left." << endl;
		// Check if they guessed the word.
		if (strcmp(word, unknown) == 0)
		{
			cout << word << endl;
			cout << "\nYeah! You got it!";
			break;
		}

	}
	if(num_of_wrong_guesses == MAX_TRIES)
	{
		cout << "\nSorry, you lose...you've been hanged." << endl;
		cout << "\nThe word was : " << word << endl;
	}
	getch();

}

/* Take a one character guess and the secret word, and fill in the
 unfinished guessword. Returns number of characters matched.
 Also, returns zero if the character is already guessed. */

int letterFill (char guess, char secretword[], char guessword[])
{
	int i;
	int matches=0;
	for (i = 0; secretword[i]!='\0'; i++)
	{

		// Did we already match this letter in a previous guess?
		if (guess == guessword[i])
			return 0;

		// Is the guess in the secret word?
		if (guess == secretword[i])
		{
			guessword[i] = guess;
			matches++;
		}
	}
	return matches;
}


// Initialize the unknown word


// Project ends here




void casino_number()

{

  char n[6];

  int balanceamt,amt,no,dice;
  char playername[80],ch;
  clrscr();
  draw_line(60,'=');
  cout<<"\n\n\n\n\t\tCASINO GAME\n\n\n\n";
  draw_line(60,'=');
  cout<<"\n\n\nEnter Your Admission id";
  cin>>n;
  cout<<"\n\nEnter Deposit amount to play game :";
  cin>>balanceamt;
  do
  {
    clrscr();
    rules();
    cout<<"\n\nYour current balance is Rs."<<balanceamt;
    do
    {
	cout<<"\n\nenter money to bet";
	cin>>amt;
	if(amt>balanceamt)
	   cout<<"Your betting amount is more than your current balance\n\nRe-enter data\n ";
	else
	   break;
    }while(1);
    do
    {
	cout<<"Enter your lucky number to bet between 1 to 12 :";
	cin>>no;
	if(no<=0||no>12)
	   cout<<"Please check the number!! should be between 1 to 12\n\nRe-enter data\n ";
	else
	   break;
    }while(1);
  randomize();
  dice=random(12)+1;
  if(dice==no)
  {
    cout<<"\n\nGood Luck!! You won Rs."<<amt*10;
    balanceamt=balanceamt+amt*10;
    score(amt,n);
  }
  else
  {
     cout<<"Bad Luck this time !! You lose Rs."<<amt;
     balanceamt=balanceamt-amt;
     score(-1*amt,n);
  }
  cout<<"\n\nThe winning number was : "<<dice;

  cout<<"\n\n\t"<<" You have Rs. "<<balanceamt<<endl;
  cout<<"\n\n-->Do you want to play (y/n)? ";
  cin>>ch;
  }while(ch=='Y'|| ch=='y');
  clrscr();
  cout<<"\n\n\n";
  draw_line(70,'+');
  cout<<"\n\n\t\THANKS FOR COME TO CASINO YOUR BALANCE AMOUNT IS RS."<<balanceamt<<"\n\n";
  draw_line(70,'+');
  cout<<"\n\nGame developed by gayathrisandeep\n";
  draw_line(70,'+');
  getch();

}
void draw_line(int n,char ch)
{
for(int i=0;i<n;i++)
   cout<<ch;
}

void rules()
{
  clrscr();
  cout<<"\n\n";
  draw_line(60,'-');
  cout<<"\n\t\tRULES OF THE GAME\n";
  draw_line(60,'-');
  cout<<"\n\t1. Choose any number between 1 to 12\n\t2. If you win you will get 10 times of money you bet\n\t3. If you bet on wrong number you will lose your betting amount\n\n";
  draw_line(60,'-');
  cout<<endl;
}


// END OF PROGRAM

void quiz()
{
clrscr();
int x,y,z;
x=y=z=0;
char ch1[100],ch2,ch3,ch4,ch5,ch6,ch7,ch8,ch9,ch10,ch11;
cout<<"        Guest Enter Your Admission id";
cin>>ch1;
clrscr();
cout<<"\n\n        Welcome ";
cout<<"\n\nEnter answer in form of ‘a','b' and'c'only.";
cout<<"\n\n\nWhat is called as ‘ THE HOLYLAND'? \na.Jerusalem\nb.Mathura\nc.Mecca";
cin>>ch2;
if(ch2=='a')
{
x=x+10;
cout<<"\n\nGood Job.Your score is "<<x;
}
else
cout<<"\n\nSorry wrong answer.";
getch();
clrscr();
cout<<"\n\nWhat is called as ‘ THE ROOF OF THE WORLD'?\na.Nepal\nb.Rome\nc.Tibet";
cin>>ch2;
if(ch2=='c')
{
x=x+10;
cout<<"\n\nGood Job.Your score is "<<x;
}
else
cout<<"\n\nSorry wrong answer.";
getch();
clrscr();
cout<<"\n\nWhat is called as ‘ THE LAND OF RISING SUN'?\na.Chicago\nb.Japan\nc.Tibet";
cin>>ch2;
if(ch2=='b')
{
x=x+10;
cout<<"\n\nGood Job.Your score is "<<x;
}
else
cout<<"\n\nSorry wrong answer.";
getch();
clrscr();
cout<<"\n\nWhat is called as ‘ THE GIFT OF NILE'?\na.Chicago\nb.Egypt\nc.Africa";
cin>>ch2;
if(ch2=='b')
{
x=x+10;
cout<<"\n\nYour score is "<<x;
}
else
cout<<"\n\nSorry wrong answer.";
getch();
clrscr();
cout<<"What is called as ‘ THE LAND OF MIDNIGHT SUN'?\na.Norway\nb.Japan\nc.Australia";
cin>>ch2;
if(ch2=='a')
{
x=x+10;
cout<<"Your score is "<<x;
}
else
cout<<"Sorry wrong answer.";
getch();
clrscr();
cout<<"What is called as ‘ THE LAND OF THUNDERBOLT'?\na.Bhutan\nb.Canada\nc.Arab";
cin>>ch2;
if(ch2=='a')
{
x=x+10;
cout<<"Your score is "<<x;
}
else
cout<<"Sorry wrong answer.";
getch();
clrscr();
cout<<"What is called as ‘ THE WINDY CITY?\na.Jerusalem\nb.Japan\nc.Chicago";
cin>>ch2;
if(ch2=='c')
{
x=x+10;
cout<<"Your score is "<<x;
}
else
cout<<"Sorry wrong answer.";
getch();
clrscr();
cout<<"What is called as ‘ THE LAND OF WHITE ELEPHANTS'?\na.Bangladesh\nb.Thailand\nc.India";
cin>>ch2;
if(ch2=='b')
{
x=x+10;
cout<<"Your score is "<<x;
}
else
cout<<"Sorry wrong answer.";
getch();
clrscr();
cout<<"What is called as ‘ THE CITY OF SEVEN HILLS'?\na.Rome\nb.Nilgiri Hills\nc.Tibet";
cin>>ch2;
if(ch2=='a')
{
x=x+10;
cout<<"Your score is "<<x;}
else
cout<<"Sorry wrong answer.";
getch();
clrscr();
cout<<"What is called as ‘ THE DARK CONTIENENT'?\na.Asia\nb.Australia\nc.Africa";
cin>>ch2;
if(ch2=='c')
{
x=x+10;
cout<<"Your score is "<<x;
}
else
cout<<"Sorry wrong answer.";
getch();
clrscr();
score(x/10,ch1);
if(x==100)
cout<<"\nGOOD!!!!!GREAT!!!!";
else if(x==90)
{cout<<"\nYou are extremely intelligent";
cout<<"\nYour Score is 90";}
else if(x==80)
{cout<<"\nYou are intelligent";
cout<<"\nYour Score is 80";}
else if(50==x||x==70||x==60)
{cout<<"\nYou are average";
cout<<"\nYour Score is "<<x<<" Better luck next time";}
else if(x<=40)
cout<<"\nNo use…….. Not even 5 questions right";
getch();
}





	 //class ends here




//***************************************************************
//    	global declaration for stream object, object
//****************************************************************

fstream fp,fp1;

student st;

//***************************************************************
//    	function to write in file
//****************************************************************
void write_student()
{
	char ch;
	fp.open("stud.dat",ios::out|ios::app);
	do
	{
		st.create_student();
		fp.write((char*)&st,sizeof(student));
		cout<<"\n\ndo you want to add more record..(y/n?)";
		cin>>ch;
	}while(ch=='y'||ch=='Y');
	fp.close();
}


//***************************************************************
//    	function to read specific record from file
//****************************************************************
void display_sps(char n[])
{
	cout<<"\nSTUDENT DETAILS\n";
	int flag=0;
	fp.open("stud.dat",ios::in);
	while(fp.read((char*)&st,sizeof(student)))
	{
		if((strcmpi(st.retadmno(),n)==0))
		{
			st.show_student();
			flag=1;
		}
	}

	fp.close();
	if(flag==0)
    		cout<<"\n\nStudent does not exist";
 	getch();
}

//***************************************************************
//    	function to modify record of file
//****************************************************************
void modify_students()
{
	char n[6];
	int found=0;
	clrscr();
	cout<<"\n\n\tMODIFY STUDENT RECORD... ";
	cout<<"\n\n\tEnter The admission id. of The student";
	cin>>n;
	fp.open("stud.dat",ios::in|ios::out);
	while(fp.read((char*)&st,sizeof(student)) && found==0)
	{
		if(strcmpi(st.retadmno(),n)==0)
		{
			st.show_student();
			cout<<"\nEnter The New Details of student"<<endl;
			st.modify_student();
			int pos=-1*sizeof(st);
			fp.seekp(pos,ios::cur);
			fp.write((char*)&st,sizeof(student));
			cout<<"\n\n\t Record Updated";
			found=1;
		}
	}

	fp.close();
	if(found==0)
		cout<<"\n\n Record Not Found ";
	getch();
}

//***************************************************************
//    	function to delete record of file
//****************************************************************


void delete_student()
{
	char n[6];
	int flag=0;
	clrscr();
    	cout<<"\n\n\n\tDELETE STUDENT...";
    	cout<<"\n\nEnter The admission id. of the Student You Want To Delete : ";
    	cin>>n;
    	fp.open("stud.dat",ios::in|ios::out);
    	fstream fp2;
    	fp2.open("Temp.dat",ios::out);
    	fp.seekg(0,ios::beg);
    	while(fp.read((char*)&st,sizeof(student)))
	{
		if(strcmpi(st.retadmno(),n)!=0)
	     		fp2.write((char*)&st,sizeof(student));
		else
	   		flag=1;
	}

	fp2.close();
    	fp.close();
    	remove("stud.dat");
    	rename("Temp.dat","stud.dat");
    	if(flag==1)
     		cout<<"\n\n\tRecord Deleted ..";
    	else
     		cout<<"\n\nRecord not found";
    	getch();
}
//***************************************************************
//    	function to display all students list
//****************************************************************

void display_alls()
{
	clrscr();
     	fp.open("stud.dat",ios::in);
     	if(!fp)
     	{
       		cout<<"ERROR!!! FILE COULD NOT BE OPEN ";
       		getch();
       		return;
     	}

	cout<<"\n\n\t\tSTUDENT LIST\n\n";
	cout<<"==================================================================\n";
	cout<<"\tAdmission Id."<<setw(10)<<"Name"<<setw(20)<<"Scores won\n";
	cout<<"==================================================================\n";

	while(fp.read((char*)&st,sizeof(student)))
	{
		st.report();
	}

	fp.close();
	getch();
}

//***************************************************************
//    	INTRODUCTION FUNCTION
//****************************************************************

void intro()
{
	clrscr();
	gotoxy(35,11);
	cout<<"SCHOOL ";
	gotoxy(35,14);
	cout<<"GAME STORE";
	gotoxy(35,17);
	cout<<"!!!!!!";
	cout<<"\n\nMADE BY : GAYATHRI SANDEEP";
   cout<<"\n\n        : RUHI ELIZABETH";
   cout<<"\n\n        : SHIVI GUPTHA";
	cout<<"\n\nSCHOOL : SARASWATHI VIDYA NIKETHAN";
	getch();
}
//***************************************************************
//    	ADMINISTRATOR MENU FUNCTION
//****************************************************************

void sub_menu()
{
	clrscr();
	int ch2;
	cout<<"\n\n\n\tSUB_MENU";
	cout<<"\n\n\t1.CREATE STUDENT RECORD";
	cout<<"\n\n\t2.DISPLAY ALL STUDENTS RECORD";
	cout<<"\n\n\t3.DISPLAY SPECIFIC STUDENT RECORD ";
	cout<<"\n\n\t4.MODIFY STUDENT RECORD";
	cout<<"\n\n\t5.DELETE STUDENT RECORD";
	cout<<"\n\n\t6.PLAY TIC TAC TOE ";
	cout<<"\n\n\t7.PLAY CASINO NUMBER";
	cout<<"\n\n\t8.PLAY QUIZ ";
	cout<<"\n\n\t9.PLAY HANG MAN ";

	cout<<"\n\n\t10.BACK TO MAIN MENU";
	cout<<"\n\n\tPlease Enter Your Choice (1-10) ";
	cin>>ch2;
	switch(ch2)
	{
    		case 1: clrscr();
	    		write_student();break;
    		case 2: display_alls();break;
    		case 3:
	       		char num[6];
	       		clrscr();
	       		cout<<"\n\n\tPlease Enter The Admission id. ";
	       		cin>>num;
	       		display_sps(num);
	       		break;
      		case 4: modify_students();break;
      		case 5: delete_student();break;
		case 6: clrscr();

			tic_tac_toe();break;
		case 7: clrscr();
		     casino_number();         break;
		case 8: clrscr();
			   quiz();
	       		break;

      		case 9: clrscr();
		     Hang_man();break;

     		case 10: return;
      		default:cout<<"\a";
   	}
   	sub_menu();
}


//***************************************************************
//    	THE MAIN FUNCTION OF PROGRAM
//****************************************************************


void main()
{
	char ch;
	intro();
	do
	{
		clrscr();
		cout<<"\n\n\n\tMAIN MENU";
             cout<<"\n\n\t01. SUB MENU";
	  	cout<<"\n\n\t02. EXIT";
	  	cout<<"\n\n\tPlease Select Your Option (1/2) ";
	  	ch=getch();
	  	switch(ch)
	  	{
			case '1':clrscr();
				 sub_menu();
			   	 break;
		  	case '2':exit(0);
		  	default :cout<<"\a";
		}
    	}while(ch!='2');
}

