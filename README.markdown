CRL Set Tools - Ready to be compliled as a python shared object file (.so)

============

The modifications I made from the original branch:

*Added export comments
	
*Added functions that can be called from python. This functions also capture all of the statements meant for Stdout and save them a file

In order to do this, I changed all of the function headers, by adding an io.Writer. If you run the program as originally designed, the writer will be Stdout. If you run the program through the new python interface, the writer will be a buffer (which will be written to a file)

(I made this modification because was having trouble reading this data easily in my project environment)
	
*Some "%s"s in the Fprintf functions, that were going to Stderr, were crashing my program, so I cut them out.
(I am fairly new to python, and VERY new to Go. This was the simplest solution for me)	
	
*Added a new function that gets the newest version number. This allowed me to deside if I need to update my local CRLset.
	
In order to build the .so file to use in python, I used this command:

	% go build -buildmode=c-shared -o crlset.so crlset.go”

In order to build the CRL-Tools to run in Go, follow the original instructions below.

============

crlset is a utility program for downloading and dumping the current Chrome CRLSet. It can be built with Go1. See http://golang.org/doc/install.html, but don't pass "-u release" when fetching the repository.

One you have Go installed, run:

    % go build crlset.go

First you need to download the current CRL set:

    % ./crlset fetch > crl-set
    Downloading CRLSet version 59

Then you can dump the contents of the CRL set:

    % ./crlset dump crl-set

Revocations are grouped by the SHA-256 hash of the issuing certificate's SubjectPublicKeyInfo and listed as serial numbers.

To also show SPKIs that have been blocked:

    % ./crlset dumpSPKIs crl-set

You can also list only the serials issued under a given certificate:

    % ./crlset dump crl-set my-ca-cert.pem
