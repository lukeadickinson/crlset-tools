CRL Set Tools
============

crlset is a utility program for downloading and dumping the current Chrome CRLSet. It can be built with Go1. See http://golang.org/doc/install.html, but don't pass "-u release" when fetching the repository.

One you have Go installed, run:

    % 6g crlset.go
    % 6l -o crlset crlset.6

First you need to download the current CRL set:

    % ./crlset fetch > crl-set
    Downloading CRLSet version 59

Then you can dump everything in the CRL set:

    % ./crlset dump crl-set

Or you can list only the serials issued under a given certificate:

    % ./crlset dump crl-set my-ca-cert.pem