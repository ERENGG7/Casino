#include <iostream>
#include<thread>
#include<chrono>
#include<cstdlib>
#include<ctime>
#include<string>
#include<stdexcept>

#define RESET "\033[0m"
#define RED "\033[31m"
#define GREEN "\033[32m"
#define YELLOW "\033[33m"
#define BLUE "\033[34m"
#define PURPLE "\033[35m"
#define CYAN "\033[36m"
#define WHITE "\033[37m"

using namespace std;

string firstName;
string lastName;
int birthday;
int monthOfBirthDay;
int yearOfBirth;
int age;

bool isCreating = true;
bool isRunning = true;
bool appOpened = true;

static string randomColor() {
	string colors[] = { RED,GREEN,YELLOW,BLUE,PURPLE,CYAN };
	int index = rand() % 6;
	return colors[index];
}
void currentTime() {
	time_t now = time(0);
	tm localtime;
	localtime_s(&localtime, &now);
	int currentYear = localtime.tm_year + 1900;
	int currentMonth = localtime.tm_mon + 1;
	int currentDay = localtime.tm_mday;
	int currentHour = localtime.tm_hour;
	int currentMinute = localtime.tm_min;

	string currentMonthIndex;
	switch (currentMonth) {
	case 1: currentMonthIndex = "Jan"; break;
	case 2: currentMonthIndex = "Feb"; break;
	case 3:currentMonthIndex = "Mar"; break;
	case 4: currentMonthIndex = "Apr"; break;
	case 5: currentMonthIndex = "May"; break;
	case 6:currentMonthIndex = "Jun"; break;
	case 7: currentMonthIndex = "Jul"; break;
	case 8: currentMonthIndex = "Aug"; break;
	case 9:currentMonthIndex = "Sep"; break;
	case 10: currentMonthIndex = "Oct"; break;
	case 11: currentMonthIndex = "Nov"; break;
	case 12:currentMonthIndex = "Dec"; break;
	}
	cout << currentHour << ':' << currentMinute
		<< ' ' << currentDay << ' ' << currentMonthIndex << ' ' << currentYear << endl;
}
void createProfile() {
	while (isCreating) {
		cout << "Enter your first name: ";
		cin >> firstName;
		cout << "Enter your lastName: ";
		cin >> lastName;
		while (true) {
			system("cls");
			cout << "Enter your birthday data:" << endl;
			cout << "Year:";
			string testYearOfBirth;
			cin >> testYearOfBirth;
			try {
				yearOfBirth = stoi(testYearOfBirth);
			}
			catch (const invalid_argument&) {
				cout << "Invalid year! ";
				system("pause>0");
				continue;
			}
			/*cin >> yearOfBirth;*/
			time_t now = time(0);
			tm localtime;
			localtime_s(&localtime, &now);
			int currentYear = localtime.tm_year + 1900;
			if (yearOfBirth < 1900 || yearOfBirth > currentYear - 1) {
				cout << "Invalid year! Enter number!" << endl;
				system("pause>0");
				continue;
			}
			else {
				break;
			}
		}
		while (true) {
			system("cls");
			cout << "Enter your birthday data" << endl;
			cout << "Year:" << yearOfBirth << endl;
			cout << "Month:";
			string testMonthOfBirthday;
			cin >> testMonthOfBirthday;
			try {
				monthOfBirthDay = stoi(testMonthOfBirthday);
			}
			catch (const invalid_argument&) {
				cout << "Invalid month! Enter number!";
				system("pause>0");
				continue;
			}
			/*cin >> monthOfBirthDay;*/

			if (monthOfBirthDay < 1 || monthOfBirthDay>12) {
				cout << "Invalid month";
				system("pause>0");
				continue;
			}
			else {
				break;
			}
		}
		while (true) {
			system("cls");
			cout << "Enter your birthday data" << endl;
			cout << "Year:" << yearOfBirth << endl;
			cout << "Month:" << monthOfBirthDay << endl;
			cout << "Day:";
			string testBirthDay;
			cin >> testBirthDay;
			try {
				birthday = stoi(testBirthDay);
			}
			catch (const invalid_argument&) {
				cout << "Invalid day! Enter number!";
				system("pause>0");
				continue;
			}
			/*cin >> birthday;*/
			if (monthOfBirthDay == 1 || monthOfBirthDay == 3
				|| monthOfBirthDay == 5 || monthOfBirthDay == 7
				|| monthOfBirthDay == 8 || monthOfBirthDay == 10
				|| monthOfBirthDay == 12) {
				if (birthday < 1 || birthday > 31) {
					cout << "Invalid day" << endl;
					system("pause>0");
					continue;
				}
				else {
					break;
				}
			}
			else if (monthOfBirthDay == 4 || monthOfBirthDay == 6
				|| monthOfBirthDay == 9 || monthOfBirthDay == 11) {
				if (birthday < 1 || birthday > 30) {
					cout << "Invalid day" << endl;
					system("pause>0");
					continue;
				}
				else {
					break;
				}
			}
			else if (monthOfBirthDay == 2) {

				if (yearOfBirth % 4 == 0 && yearOfBirth % 100 != 0) {
					if (birthday < 1 || birthday > 29) {
						cout << "Invalid day" << endl;
						system("pause>0");
						continue;
					}
					else {
						break;
					}
				}
				else {
					if (birthday < 0 || birthday > 29) {
						cout << "Invalid day" << endl;
						system("pause>0");
						continue;
					}
					else {
						break;
					}
				}
			}
		}
		time_t now = time(0);
		tm localtime;
		localtime_s(&localtime, &now);
		int yearNow = localtime.tm_year + 1900;
		age = yearNow - yearOfBirth;
		if (age < 18) {
			cout << "Sorry but you cant use this app" << endl;
			isCreating = false;
			appOpened = false;
			isRunning = false;
			return;
		}
		else {
			cout << "Congratuelations. You created profile.You start balance is 100." << endl;
			isCreating = false;
		}
	}
}

int main() {
	srand(time(0));
	int balance = 100;
	string input;
	int bet;
	int totalPrise = 0;
	char symb;
	while (appOpened) {

		createProfile();

		while (isRunning) {
			system("cls");
			cout << PURPLE << "Hello:" << firstName << ' ' << lastName << RESET << endl;
			cout << YELLOW << "Enter number bigger from your balance to quit" << endl;
			cout << "Balance: " << balance << endl;
			cout << "Enter bet:";
			cin >> input; RESET;
			try {
				bet = stoi(input);
			}
			catch (const invalid_argument&) {
				cout << RED << "Invalid bet! Enter number!" << RESET << endl;
				this_thread::sleep_for(chrono::seconds(1));
				continue;
			}

			if (bet <= 0) {
				cout << RED << "Invalid bet" << RESET << endl;
				this_thread::sleep_for(chrono::seconds(1));
				continue;
			}
			else if (balance < bet) {
				cout << RED << "Not enough money" << RESET << endl;
				this_thread::sleep_for(chrono::seconds(1));
				isRunning = false;

			}
			else {
				int a = rand() % 9 + 1;
				int b = rand() % 9 + 1;
				int c = rand() % 9 + 1;
				cout << randomColor() << a << RESET
					<< ' ' << randomColor() << b << RESET
					<< ' ' << randomColor() << c << RESET << ' ' << endl;

				if (bet >= 1000) {
					if (a == 7 && b == 7 && c == 7) {
						cout << YELLOW << "777 JACKPOT 777" << endl;
						cout << "Prise: " << bet * 100 << RESET << endl;
						balance += bet * 100;
						totalPrise += bet * 100;
					}
					else if (a == b && b == c) {
						cout << YELLOW << "JACKPOT" << endl;
						cout << "Prise: " << bet * 100 << RESET << endl;
						balance += bet * 100;
						totalPrise += bet * 100;
					}
					else if ((a == 7 && b == 7) || (b == 7 && c == 7) || (a == 7 && c == 7)) {
						cout << YELLOW << "BIG WIN" << endl;
						cout << "Prise: " << bet * 10 << RESET << endl;
						balance += bet * 10;
						totalPrise += bet * 10;
					}
					else if (a == 7 || b == 7 || c == 7) {
						cout << YELLOW << "7 X WILD" << endl;
						cout << "Prise: " << bet * 7 << RESET << endl;
						balance += bet * 7;
						totalPrise += bet * 7;
					}
					else if (a == b || b == c || a == c) {
						cout << YELLOW << "WINNER" << endl;
						cout << "Prise: " << bet * 2 << RESET << endl;
						balance += bet * 2;
						totalPrise += bet * 2;
					}
					else {
						cout << YELLOW << "Try again" << RESET << endl;
						balance -= bet;
						totalPrise -= bet;
						if (totalPrise < 0) {
							totalPrise = 0;
						}
					}
				}
				else {
					if (a == b && b == c) {
						cout << YELLOW << "JACKPOT" << endl;
						cout << "Prise: " << bet * 100 << RESET << endl;
						balance += bet * 100;
						totalPrise += bet * 100;
					}
					else if (a == b || b == c || a == c) {
						cout << YELLOW << "WINNER" << endl;
						cout << "Prise: " << bet * 2 << RESET << endl;
						balance += bet * 2;
						totalPrise += bet * 2;
					}
					else {
						cout << YELLOW << "Try again" << RESET << endl;
						balance -= bet;
						totalPrise -= bet;
						if (totalPrise < 0) {
							totalPrise = 0;
						}
					}
				}
				system("pause>0");
			}
		}
		cout << YELLOW << "Your win total:" << totalPrise << RESET << endl;
		currentTime();
		system("pause>0");
		appOpened = false;
	}
	return 0;
}