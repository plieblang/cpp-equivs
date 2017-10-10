All of this assumes using namespace std;

# Class equivalents
cin/cout
	#include <iostream>
	
string:
	#include <string>

arraylist:
	#include <vector>
	vector<int> v;

# Method equivalents
to skip blank line of input:
	string blank;
	getline(cin, blank)
	
substring:
	string line = "test";
	line.substr(0,2);//produces "tes"
	inclusive at the beginning, excusive at the end
	
read a line with spaces into a string:
	string line;
	cin.ignore()//flushes newline
	getline(cin, line)
	
sorting a vector:
	#include <algorithm>
	sort(v.begin(), v.end());
