brazil
======

Usage
-----

::

     . brazil.sh to load the function

This maintains the ~/.ssh/config file and \* a comment with the format
*#:alias:hostname:identityfile * It also creates a host IdentityFile
entry example :sub:`~`

brazil ssh *alias*
------------------

brazil list
-----------

show the aliases and hostnames

brazil add
----------

-  Adds or replaces the entry in ~/.amazon
-  adds an entry to ~/.ssh/config ### example brazil add aliasName
   hostname pemfile

brazil ssh *alias*
------------------

-  ssh ec2-user@hostname

brazil sethost *alias*
----------------------

export host=\ **hostname**

::

    brazil() {
        alias_file=~/.ssh/config

        cmd=$1
        export alias=$2
        echo cmd is $cmd alias is $alias
        the_hostnm=`awk -F: '{if ($2 == "'$alias'")  {print $3; exit}}' $alias_file`
        if [ $cmd == 'add' ] ; then  
            if [ $# -ne 4 ] ; then 
                echo usage add alias hostname pemfile 2>&1
                return 0
            fi
            alias=$2
            host_nm=$3
            pem=$4

-  ensure the identify file exist and set permissions
   identity\_file=~/.ssh/\ :math:`{pem}             if [ ! -f `\ identity\_file
   ] ; then echo
   :math:`identity_file does not exist 2>&1                 return 1             else                  chmod 600 `\ identity\_file
   fi
-  is the alias in the file? grep "#::math:`{alias}:"  `\ {alias\_file}
   # TODO need a bettter pattern if [ $? -eq 1 ] ; then # not present
   add echo adding :math:`alias `\ hostname
   :math:`pem                 echo "#:`\ {alias}::math:`{host_nm}:`\ {pem}"
   >> :math:`alias_file                  echo Host `\ {host\_nm} >>
   ~/.ssh/config echo " IdentityFile
   ./.ssh/\ :math:`identity_file"                 echo pem is `\ pem
   echo " IdentityFile
   ~/.ssh/\ :math:`{pem}" >> ~/.ssh/config              else                  echo changing hostname for  `\ alias
   :math:`hostname `\ pem sed -i -e
   "s/:.*/::math:`{host_nm}/" `\ {alias\_file} sed -i -e
   "s/:.*/::math:`{host_nm}/" ~/.ssh/config             fi                 chmod 600 ~/.ssh/config              echo "~/.ssh/config"             cat ~/.ssh/config         else              if [ -z `\ the\_hostnm
   ] ; then set +x echo alias
   :math:`alias not found in: >&2                  cat ~/.ssh/config >&2             else                  echo the_hostnm is `\ the\_hostnm
   case
   :math:`cmd in                     "ssh")                         if [ `\ #
   -ne 2 ] ; then echo "usage brazil ssh alias" 2>&1 return 1 fi echo
   connecting to :math:`alias `\ {the\_hostnm} ssh
   ec2-user@\ :math:`{the_hostnm} ;;                    "list")                          cat ~/.ssh/config ;;                    "edit")                         vim ~/.ssh/config                          . ~/bin/brazil.sh ;;                    "scp")                         set -x                        last_arg=`\ {@::math:`#}                        arg_count=`\ #
   echo arg\_count
   :math:`{arg_count}                        leading_arg_count=`expr `\ {arg\_count}
   - 2\` echo leading\_arg\_count
   :math:`{leading_arg_count}                        leading_args=`\ {@:1::math:`{leading_arg_count}}                        echo leading_args `\ {leading\_args}
   echo last\_arg
   :math:`last_arg                        echo scp `\ leading\_args
   ec2-user@\ :math:`{the_hostnm}:`\ {last\_arg} ;; "sethost") export
   amazon="\ :math:`{the_hostnm}"                        echo host set to `\ {the\_hostnm}
   ;; \*) echo usage "brazil command args" echo "command is sethost edit
   list ssh add" ;; esac fi fi }

alias braziladd="brazil add" alias brazilssh="brazil ssh" alias
brazilhost="brasil sethost" alias brazillist="brazil list"
