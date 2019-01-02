All of this assumes using namespace std;

# Compilation

Contest:

	g++ -g -O2 -std=gnu++14
	
universal include

	//Available with GCC, not MSVC
	#include <bits/stdc++.h>

# Classes
cin/cout:

	#include <iostream>
	ios_base::sync_with_stdio(false);
    cin.tie(NULL);

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
	
useful include headers

	#include <iostream>
	#include <string>
	#include <vector>
	#include <utility>
	#include <unordered_map>
	#include <unordered_set>
	#include <queue>
	#include <stack>
	#include <algorithm>
	#include <cmath>
	#include <climits>
	#include <functional>
	
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

pair:

	pair<int, int> p = make_pair(1, 2);

creating a members of a class with that class type:

	class clazz{
		clazz* c;
	}
	
constructors

	Clazz c()
	Creates a class with automatic storage duration; ie it is cleaned up automatically
	Allocates to stack
	Fast
	Sacrifices flexibility because you must know the exact quantity, lifetime, and type of objects while you’re writing the program.
	
	Clazz *c = new Clazz()
	Creates a class with dynamic storage duration and must be manually deleted
	Returns a pointer to the instantiated object
	Allocates to heap
	Slower than allocating to stack
	Example use case is for an array where size isn't known at compile time

# Methods
printing to n decimal places with cout:

	#include <iomanip>
	double d = 17.1717171717;
	//this rounds
	cout << setprecision(1) << fixed << d;

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
	//TODO check whether this is correct
	//https://stackoverflow.com/questions/25475384/when-and-why-do-i-need-to-use-cin-ignore-in-c#25476169
	//cin.ignore();
	getline(cin, line);
	
get index of first occurrence of a substring in a string:

	string s = "thisbetest";
	//6
	//returns string::npos (size_t type) if the substring isn't found
	s.find("test");
	
split string on space:

	#include <sstream>
	#include <iterator>
	#include <vector>
	#include <string>
	
	string line;
	while(getline(cin, line)){
		istringstream ss(line);
		//change the generic types of the istream_iterator and the vector to split into ints, chars, etc.
		istream_iterator<string> begin(ss), end;
		vector<string> tokens(begin, end);
	}
	
vector size:

	vector<int> v;
	v.size();
	
sorting a vector:

	//sorts vector of strings as well
	sort(v.begin(), v.end());
	
sort a vector in reverse:

	sort(v.begin(), v.end(), less<int>());
	
sorting lists of items by nth element

	//IMPORTANT:  this variable must be global so that the lambda can see it
	//also cannot be passed to a comparison function
	int keyIdx = 2;
	
	vector<vector<int>> vec;
	for (int i = 0; i < 50; i++) {
		vector<int> temp;
		for (int i = 0; i < 25; i++) {
			temp.push_back(rand());
		}
		vec.push_back(temp);
	}

	sort(vec.begin(), vec.end(), [](vector<int> &v1, vector<int> &v2) {
		return v1[keyIdx] < v2[keyIdx];
	});

remove item at index from vector:

	//v contains numbers from 0-20
	//removes the index + 1 item, in this case 17
	v.erase(v.begin() + 17);

remove value from vector

	TODO
	distVec.erase(remove(distVec.begin(), distVec.end(), v), distVec.end());

accessing items in a pair:

	pair<int, int> p = make_pair(1, 2);
	cout << pair.first << pair.second;

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

adding to priority queue

	priority_queue<int> pq;
	pq.push(5);

popping from priority queue

	priority_queue<int> pq;
	//add stuff
	int x = pq.top();
	//pop() removes the item without returning it
	pq.pop()
	
priority queue with custom comparator

	auto comparator = [](vector<int> v1, vector<int> v2) {
		return v1[1] > v2[1];
	};
	priority_queue<vector<int>, vector<vector<int>>, decltype(comparator)> q(comparator);
	for (int i = 0; i < 50; i++) {
		vector<int> v;
		for (int j = 0; j < 5; j++) {
			v.push_back(10000 - j * i);
		}
		q.push(v);
	}

INT_MIN and INT_MAX:

	#include <climits>
	
accumulate

	#include <numeric>
	TODO

the cmath header

the functional header