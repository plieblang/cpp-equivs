All of this assumes using namespace std;

# Classes
cin/cout:

	#include <iostream>

printf:

	#include <stdio.h>
	int x = 5;
	printf("%d", x);
	double y = 5.5555555;
	printf("%.3f", y);//prints to 3 decimal places and rounds
	
string:

	#include <string>

arraylist:

	#include <vector>
	vector<int> v;

hashmap:

	//c++11 and above
	//have had trouble with g++ not recognizing it
	//apparently the fix is to change the include header and namespace declaration to:
	//#include <tr1/unordered_map>
	//using namespace std::tr1;
	#include <unordered_map>
	unordered_map<int, int> dict;

can also use map:

	//slower than unordered_map
	#include <map>
	map<int, int> dict;

array class (only C++11 and above):

	//n.b.
	//I don't believe this can be instantiated without knowing the values beforehand
	//so a vector is probably more useful in most situations
	#include <array>
	int size = 5;
	array<int, size> arr = {0, 1, 2, 3, 4};
	array<int, size> arr{{0, 1, 2, 3, 4}}//double curly braces not needed for c++14

creating a members of a class with that class type

	class clazz{
		clazz* c;
	}
	
constructors

	Clazz c()
	Creates a class with automatic storage duration; ie it is cleaned up automatically
	Allocates to stack
	Fast
	Sacrifices flexibility because you must know the exact quantity, lifetime, and type of objects while you’re writing the program.
	
	new Clazz()
	Creates a class with dynamic storage duration and must be manually deleted
	Returns a pointer to the instantiated object
	Allocates to heap
	Slower than allocating to stack
	Example use case is for an array where size isn't known at compile time

# Methods
printing to n decimal places with cout:

	double d = 5.55555;
	int precision = 3;
	cout.precision(precision);
	//this rounds
	cout << d;

to skip blank line of input:

	string blank;
	getline(cin, blank)
	
substring:

	string line = "test";
	line.substr(0,2);//produces "te"
	inclusive at the beginning, exclusive at the end
	
string length:

	string str = "test";
	cout << str.length();//prints 4
	
string to int:

	string str = "1965";
	int strAsInt = stoi(str);

getting a char from a string at an index:

	string str = "abc";
	int idx = 0;
	char c = str.at(idx);
	
read a line with spaces into a string:

	string line;
	cin.ignore();//flushes newline
	getline(cin, line);
	
split string:

	#include <sstream>  //for std::istringstream
	#include <iterator> //for std::istream_iterator
	#include <vector>
	#include <string>
	
	string line;
	while(getline(cin, line)){
		istringstream ss(line);
		istream_iterator<std::string> begin(ss), end;

		//putting all the tokens in the vector
		vector<string> arrayTokens(begin, end);

		cout << arrayTokens[0];
	}
	
sorting a vector:

	#include <algorithm>
	sort(v.begin(), v.end());