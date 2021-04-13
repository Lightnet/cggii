

















```c++
#include <algorithm> //need this for replace string
#include <iostream>
#include <string>

using std::cout;
//using std::cin;
using std::endl;
//using std::string;
//using std::replace;


  string spath = "C:\\test\\myfile.txt";
  replace( spath.begin(), spath.end(), '\\', '/' );
  //cout << s << endl;
  std::cout << spath << std::endl;
  printf("DIR: %s\n",spath.c_str());
```