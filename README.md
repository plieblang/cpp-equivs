All of this assumes using namespace std;

# Compilation

Contest:

	g++ -g -O2 -std=gnu++14

# Classes
cin/cout:

	#include <iostream>

printf:

	#include <stdio.h>
	int x = 17;
	printf("%d", x);
	double y = 17.17171717;
	printf("%.3f", y);//prints to 3 decimal places and rounds

printf variable formatters:

	%s:  strings
	%d:  integers
	%l:  long integer
	%ld:  long integers
	%f:  float
	
string:

	#include <string>

resizable array:

	#include <vector>
	vector<int> v;

hashmap/dictionary:

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

	double d = 17.1717171717;
	int precision = 3;
	cout.precision(precision);
	//this rounds
	cout << d;

to skip blank line of input:

	string blank;
	getline(cin, blank)
	
substring:

	//Very important
	//The first parameter is the starting index (inclusive)
	//the second parameter is the length of the desired substring
	//NOT the ending index
	string line = "test";
	line.substr(0, 2);//produces "te"
	line.substr(1, 2);//produces "es"

replace character in string:

	string str = "This test";
	//Becomes "Thin test"
	str.replace(str.begin() + 3, str.begin() + 4, "n");
	
string length:

	string str = "test";
	cout << str.length();//prints 4
	
string to int:

	//C++11 only
	int strAsInt = stoi("17");

int to string:

	//C++11 only
	string str = to_string(17);

getting a char from a string at an index:

	string str = "abc";
	int idx = 0;
	char c = str.at(idx);
	
read a line with spaces into a string:

	string line;
	//flushes newline by ignoring every character up until newline
	cin.ignore();
	getline(cin, line);
	
get index of first occurrence of a substring in a string:

	string s = "thisbetest";
	//6
	//returns string::npos (size_t type) if the substring isn't found
	s.find("test");
	
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
	
vector size:

	vector<int> v;
	v.size();
	
sorting a vector:

	//sorts vectors of strings as well
	#include <algorithm>
	sort(v.begin(), v.end());

copying a vector:

	vector<int> v1;
	//add ints to v1;
	//deep copy
	vector<int> v2 = v1;

remove item at index from vector:

	//v contains numbers from 0-20
	//removes the index + 1 item, in this case 17
	v.erase(v.begin() + 17);

check if unordered map contains key:

	unordered_map<int, int> dict;
	int key = 17;
	if(dict.count(key)){
		//dict contains 17
	}

add item to unordered map*:

	unordered_map<int, int> *dict = new unordered_map<int, int>();
	dict->insert(make_pair(17, 17));

get item from unordered map*:

	unordered_map<int, int> *dict = new unordered_map<int, int>();
	//add things; see above
	dict->at(17);

loop through unordered map:

	unordered_map<int, int> dict;
	for(auto x : dict){
		//key
		cout << x.first;
		//value
		cout << x.second;
	}

INT_MIN and INT_MAX:

	#include <climits>

exponents:

	#include <math.h>
	//integrals (ie ints, chars, etc) will be cast to doubles
	double base = 17;
	double exp = 2;
	pow(base, exp);//289

square root:

	#include <math.h>
	//integrals (ie ints, chars, etc) will be cast to doubles
	double x = 289;
	17
	sqrt(x);

log and log2:

	TODO

ceiling and floor

	TODO
