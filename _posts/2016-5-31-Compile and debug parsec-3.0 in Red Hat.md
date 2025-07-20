---
layout: post
title: Compile and Debug PARSEC-3.0 in Red Hat
tags: GEM5 Benchmark 

---
### Download

Download parsec-3.0 from its [official website](http://parsec.cs.princeton.edu/download.htm).

### Compile

Decompress the parsec-3.0 compressed file, and compile it using the following instruct:

    sudo ./bin/parsecmgmt -a build
	
### Debug

1. ERROR 1: pod2man error

        POD document had syntax errors at /usr/bin/pod2man line 69.  
        make: *** [install_docs] Error 1   
        [PARSEC] Error: 'env PATH=/usr/bin:/home/gem5/parsec-3.0/bin:/sbin:/bin:/usr/sbin:/usr/bin /usr/bin/make install' failed.   
	
   Solution: delete pod2man file
  
        sudo rm /usr/bin/pod2man
	  
2. ERROR 2: conflicting types for __mbstate_t
    
        /usr/include/wchar.h:94:3: error: conflicting types for ?._mbstate_t?
        } __mbstate_t;
  
   Solution: delete the 4 lines of code from 102 line to 105 line in the file '/parsec-3.0/pkgs/libs/uptcpip/src/include/sys/bsd__types.h'. The deleted content is shown below.

        typedef union {
           char            __mbstate8[128];
            __int64_t       _mbstateL;      /* for alignment */
        } __mbstate_t;   

3. ERROR 3: tbb failed

         Error: 'env version=tbb /usr/bin/make' failed.

   Solution: 

        yum -y install -y tbb
   
4. ERROR 4: No package 'xt' found

        No package 'xt' found

   Solution:
        
        yum -y install libXt-devel
		yum -y install libXmu-devel

5. ERROR 5: No package 'xi' found

        No package 'xi' found

   Solution:
        
        yum -y install libXi-devel
	 
   

     


