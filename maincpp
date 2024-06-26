#include<iostream>
#include<fstream>
#include<sstream>
#include<string>
#include<string.h>
using namespace std;
// functions we will use 
void readFile(string);
void breakintowords(string , string);
bool checkfornonAlphabatic(string);
bool ignoreWords(string);
void countAllthings();
bool menu(string& s) {
	int choice;
	cout << "Select choice\n Press 1 for User input\nPress 2 for file input";
	cin >> choice;
	if (choice == 1) {
		string sentence;
		cout << "Enter sentence :";
		cin.ignore();
		getline(cin, sentence);
		s = sentence;
		breakintowords(sentence, "AfterRemoval.txt");
		return false;
	}
	else if (choice == 2) {
		string fname;
		cout << "ENter file name";
		cin >> fname;
		readFile(fname);
		return true;
	}
}
void checkinDictionary(string word , int &pos , int &neg , int &total) {
	ifstream file("Dictionary.txt");
	string data;
	if (!ignoreWords(word) && checkfornonAlphabatic(word) == true)
	{
		while (getline(file, data))
		{
			string word2;
			istringstream iss(data);
			iss >> word2;
			if (word2 == word) {
				iss >> word2;
				total = total + stoi(word2);
				iss >> word2;
				pos = pos + stoi(word2);
				iss >> word2;
				neg = neg + stoi(word2);
				break;
			}
		}
	}
}
int main()
{
	string s;
	bool x = menu(s);  // all data has been written into the dictionary
	// Now output is the sentence positice or negetive 
	ifstream file("raw.txt");
	string data;
	if (x) {
		while (getline(file, data))
		{
			istringstream iss(data);
			string word;
			int positive = 0;
			int negetive = 0;
			int total = 0;
			while (iss >> word) {
				checkinDictionary(word, positive, negetive , total);
			}
			data = data.substr(2);
			cout << "\nText is : " << data << endl;
			cout << "Without Normalization\n";
			cout << "positive Count : " << positive << endl;
			cout << "Negetive Count : " << negetive << endl;
			(positive > negetive) ? cout << "Text is Positive" << endl : cout << "Text is negetive" << endl;

			if (total != 0) {
				cout << positive << endl;
				cout << negetive << endl;
				cout << total;
				double positiveWithNormalization = (positive) / (total);
				double negetiveWithNormalization = (negetive) / (total);
				cout << "\nWith Normalization\n";
				cout << "positive Count : " << positiveWithNormalization << endl;
				cout << "Negetive Count : " << negetiveWithNormalization << endl;
				(positiveWithNormalization > negetiveWithNormalization) ? cout << "Text is Positive" << endl : cout << "Text is negetive" << endl;
			}
		}
	}
	else {
		data = s;
		istringstream iss(data);
		string word;
		int positive = 0;
		int negetive = 0;
		int total = 0;
		while (iss >> word) {
			checkinDictionary(word, positive, negetive, total);
		}
		data = data.substr(2);
		cout << "\nText is : " << s << endl;
		cout << "Without Normalization\n";
		cout << "positive Count : " << positive << endl;
		cout << "Negetive Count : " << negetive << endl;
		(positive > negetive) ? cout << "Text is Positive" << endl : cout << "Text is negetive" << endl;

		if (total != 0) {
			cout << positive << endl;
			cout << negetive << endl;
			cout << total;
			double positiveWithNormalization = (positive) / (total);
			double negetiveWithNormalization = (negetive) / (total);
			cout << "\nWith Normalization\n";
			cout << "positive Count : " << positiveWithNormalization << endl;
			cout << "Negetive Count : " << negetiveWithNormalization << endl;
			(positiveWithNormalization > negetiveWithNormalization) ? cout << "Text is Positive" << endl : cout << "Text is negetive" << endl;
		}
	}
	return 0;
}
bool checkfornonAlphabatic(string word) {
	for (int i = 0; i < word.size(); i++)
		if (!((word[i] >= 'A' && word[i] <= 'Z') || (word[i] >= 'a' && word[i] <= 'z')))
			return false;
	return true;
}
bool ignoreWords(string word) {
	ifstream file("Stopwords.txt");
	if (!file) {
		cout << "FIle does not exist";
		return false;
	}
	string data;
	while (getline(file, data)) {
		if (data == word) return true;
	}
	return false; // means not a ignoredWord(keyword)
}
void breakintowords(string str , string filename) {
	ofstream WritingFile("AfterRemoval.txt", ios::app); // open in append mod
	WritingFile << str[0] << " "; // write either 1 or 0
	str = str.substr(2);
	istringstream iss(str);
	string word;
	while (iss >> word) { 
		if (checkfornonAlphabatic(word) == true) // means it is not alphabatic
		{ 
			if (!ignoreWords(word)) 	// if not a ignoreword add it to file  
			{
				WritingFile << word << " ";
			}
		}
	}
}
// read file 
void readFile(string filename) {
	ifstream file(filename);
	if (!file) {
		cout << "Unable to open the file\n";
		return;
	}
	string data;
	while (getline(file, data)) {
		ofstream WritingFile("AfterRemoval.txt", ios::app); // open in append mod
		breakintowords(data , "AfterRemoval.txt");
		WritingFile << "\n";
	}
	// After removal of all words we have new file we will use that to make a positive , total and negetive count
	countAllthings();
}
bool IsAlreadyExist(string word) {
	ifstream file("Dictionary.txt");
	string data;
	while (getline(file, data)) {
		istringstream iss(data);
		string dicWord;
		iss >> dicWord;
		if (dicWord == word) {
			return true;
		}
	}
	return false;
}
void helperfunction(string word , int &pos , int &neg , int &total) {
	ifstream file("AfterRemoval.txt");
	string data;
	while (getline(file, data)) {
		int Pos_or_Negetive = data[0] - '0'; // 0 or 1 (1 +ive)
		istringstream iss(data);
		string word2;
		while (iss >> word2) 
		{
			if (word == word2 && IsAlreadyExist(word) == false) 
			{
				if (Pos_or_Negetive == 1) 
					pos++;
				else if (Pos_or_Negetive == 0) 
					neg++;
				total++;
			}
		}
	}
}
void countAllthings() {
	ifstream file("AfterRemoval.txt");
	string data;
	while (getline(file , data)) {
		string data2 = data.substr(2); // ignore 0 , 1
		istringstream iss(data2);
		string word;
		while (iss >> word) {
			int total = 0;
			int pos = 0;
			int neg = 0;
			helperfunction(word , pos , neg , total);
			// write this into dictionary
			ofstream DictionaryWrite("Dictionary.txt", ios::app); // ios::app mean open in append mode 
			if (total != 0) {
				DictionaryWrite << word << " " << total << " " << pos << " " << neg << "\n";
			}
		}
	}
}
