make-crypto-usb
===============

if [ $# -ne 2 ] ; then echo usage: make-crypto-usb.sh device disklabel
fi

if [ -z $SECRET ] ; then echo export SECRET 2>&1 exit 1 fi

| set -x
| DEVICE=$1 DISKLABEL=$2

if [ ! -f $DEVICE ] ; then
==========================

echo no such device $DEVICE
===========================

exit 1
======

fi
==

sudo cryptsetup --verbose luksFormat :math:`DEVICE <<:EOF: `\ SECRET
:EOF:

verify
======

sudo cryptsetup luksDump :math:`DEVICE <<:EOF: `\ SECRET :EOF:

if [ $? -ne 0 ] ; then echo problem with device
:math:`DEVICE     exit else      echo found encrypted device `\ DEVICE
fi

open
====

FNAME=\ ``basename $DEVICE`` sudo cryptsetup luksOpen
:math:`DEVICE `\ FNAME <<:EOF: $SECRET :EOF:

make file system
================

mapper\_name=\ ``basename $DEVICE`` sudo mkfs -t ext4
/dev/mapper/${mapper\_name}

label it
========

sudo e2label
/dev/mapper/:math:`{DISKLABEL}` echo diskname is `\ DISKNAME

if [ ! -d /disk/$DISKNAME ] ; then sudo mkdir
/disk/:math:`DISKNAME fi # mount  sudo mount /dev/mapper/`\ FNAME
/disk/$DISKNAME
