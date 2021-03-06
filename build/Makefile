# Makefile for WWW subdirectory.

STABLE_VERSION=	6.0
PREV_VERSION=	5.9

# also update mirrors/openbgpd-ftp.html.head
OPENBGPD_VERSION=		4.6

# also update mirrors/openntpd-ftp.html.head
OPENNTPD_PORTABLE_VERSION=	6.0p1

OPENSSH_VERSION=		7.4
OPENSSH_PORTABLE_VERSION=	7.4p1

all: ../groups.html ../support.html ../ftp.html

# Build the user groups page.
../groups.html:	groups.dat groups.awk groups.skel Makefile mkcountries
		sh mkcountries groups.dat > groups.countries
		awk -f groups.awk groups.dat > groups-tbl.html
		m4 groups.skel > ../groups.html
		@rm -f groups-tbl.html groups.countries

# Build the support/consultants page.
../support.html: support.dat support.awk support.skel Makefile mkcountries
		sh mkcountries support.dat > support.countries
		awk -f support.awk support.dat > support-tbl.html
		m4 support.skel > ../support.html
		@rm -f support-tbl.html support.countries

# Build the FTP/HTTP/RSYNC mirrors page.
../ftp.html ftp: mirrors.pl mirrors.dat mirrors/ftp.html.{end,head,mid1,mid2} \
     mirrors/openntpd-portable.html.{head,end} \
     mirrors/openbgpd-ftp.html.{end,head}
	perl mirrors.pl openbsd-ftp ${STABLE_VERSION}
	perl mirrors.pl openbgpd-ftp ${OPENBGPD_VERSION}
	perl mirrors.pl openntpd-portable ${OPENNTPD_PORTABLE_VERSION}
	perl mirrors.pl openssh-ftp ${OPENSSH_VERSION}
	perl mirrors.pl openssh-portable ${OPENSSH_PORTABLE_VERSION}
	perl mirrors.pl ftplist ${STABLE_VERSION}

anoncvs: mirrors.pl mirrors.dat mirrors/anoncvs.html.{end,head}
	perl mirrors.pl anoncvs ${STABLE_VERSION}

cvsync: mirrors.pl mirrors.dat mirrors/cvsync.html.{end,head}
	perl mirrors.pl cvsync ${STABLE_VERSION}

clean:
	rm -f *.countries
