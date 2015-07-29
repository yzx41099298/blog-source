title: "Protobuf Micro"
date: 2015-03-11 17:56:39
tags:
---

###Install:

1.  Download protomicro at: https://code.google.com/p/micro-protobuf/

2. $ ./configure

3. $ make

    If errors as below：
    make[2]: *** [message.lo] Error 1
    make[1]: *** [all-recursive] Error 1
    make: *** [all] Error 2

    Add  "#include <istream>" in src/google/protobuf/message.cc

4. Create file protoc in /usr/local/bin/
    $ make install


###USAGE:

1. Define .proto file

2. Create a java class in out_dir.
    $ /usr/local/bin/protoc —-javamicro_out="our_dir" ***.proto

3. Use the java class。 

4. Import com.google.protobuf.micro in micro-protobuf-read-only/java/src/main/java/。