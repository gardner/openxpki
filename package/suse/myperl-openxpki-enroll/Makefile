## Written 2006 by Martin Bartosch for the OpenXPKI project
## Copyright (C) 2005-2011 by The OpenXPKI Project

TOPDIR=../../..

# Makefile.inc contains common settings for all packages (checked in)
include ../Makefile.inc
# Makefile.local may be used locally to override settings (not checked in)
-include ../Makefile.local

PACKAGE=myperl-openxpki-enroll
SRCBASE=$(TOPDIR)/clients/perl/OpenXPKI-Client-Enrollment
SRCNAME=$(PACKAGE)

OXI_TARBALL = $(shell rpm --eval '%{_topdir}')/SOURCES/$(PACKAGE)-$(OXI_VERSION).tar.gz
OXI_TARBALL_DIR = $(shell rpm --eval '%{_topdir}')/BUILD/tmp/$(PACKAGE)-$(OXI_VERSION)

all: clean package

$(PACKAGE).spec: $(PACKAGE).spec.template

package: $(PACKAGE).spec $(OXI_TARBALL)
	PERL_LOCAL_LIB_ROOT= PERL_MB_OPT= PERL_MM_OPT= rpmbuild -ba $(PACKAGE).spec

collect:
	mv $(RPMBASE)/SRPMS/$(PACKAGE)-*.rpm .
	mv $(RPMBASE)/RPMS/*/$(PACKAGE)-*.rpm .

clean:
	rm -f $(PACKAGE)-*.rpm $(PACKAGE).spec $(OXI_TARBALL)

$(OXI_TARBALL):
	rm -rf $(OXI_TARBALL_DIR)
	mkdir -p $(OXI_TARBALL_DIR)
	(cd ../../.. && tar cf - \
		ISSUES LICENSE README.pod clients config core doc package qatest tools) \
		| tar xf - -C $(OXI_TARBALL_DIR)
	echo $(OXI_VERSION) > $(OXI_TARBALL_DIR)/VERSION
	tar czf $@ -C $(OXI_TARBALL_DIR)/.. .

