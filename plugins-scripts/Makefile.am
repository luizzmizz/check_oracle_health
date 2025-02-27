## Process this file with automake to produce Makefile.in

SUFFIXES = .pl .pm .sh

VPATH=$(top_srcdir) $(top_srcdir)/plugins-scripts $(top_srcdir)/plugins-scripts/t

libexec_SCRIPTS=check_oracle_health
MY_MODULES=
EXTRA_MODULES=\
  Nagios/DBD/Oracle/Server/Instance/SGA/DataBuffer.pm \
  Nagios/DBD/Oracle/Server/Instance/SGA/SharedPool/DictionaryCache.pm \
  Nagios/DBD/Oracle/Server/Instance/SGA/SharedPool/LibraryCache.pm \
  Nagios/DBD/Oracle/Server/Instance/SGA/SharedPool.pm \
  Nagios/DBD/Oracle/Server/Instance/SGA/RollbackSegments.pm \
  Nagios/DBD/Oracle/Server/Instance/SGA/RedoLogBuffer.pm \
  Nagios/DBD/Oracle/Server/Instance/SGA/Latch.pm \
  Nagios/DBD/Oracle/Server/Instance/SGA.pm \
  Nagios/DBD/Oracle/Server/Instance/PGA.pm \
  Nagios/DBD/Oracle/Server/Instance/Event.pm \
  Nagios/DBD/Oracle/Server/Instance/Enqueue.pm \
  Nagios/DBD/Oracle/Server/Instance/Session.pm \
  Nagios/DBD/Oracle/Server/Instance/Sysstat.pm \
  Nagios/DBD/Oracle/Server/Instance/SysTimeModel.pm \
  Nagios/DBD/Oracle/Server/Instance/SysWaitClass.pm \
  Nagios/DBD/Oracle/Server/Instance.pm \
  Nagios/DBD/Oracle/Server/Database/User.pm \
  Nagios/DBD/Oracle/Server/Database/Dataguard.pm \
  Nagios/DBD/Oracle/Server/Database/FlashRecoveryArea.pm \
  Nagios/DBD/Oracle/Server/Database/Tablespace/Datafile.pm \
  Nagios/DBD/Oracle/Server/Database/Tablespace/Segment.pm \
  Nagios/DBD/Oracle/Server/Database/Tablespace.pm \
  Nagios/DBD/Oracle/Server/Database/Asm/Diskgroup.pm \
  Nagios/DBD/Oracle/Server/Database/Asm.pm \
  Nagios/DBD/Oracle/Server/Database.pm \
  Nagios/DBD/Oracle/Server.pm \
  Nagios/Extraopts.pm
EXTRA_DIST=check_oracle_health.pl $(EXTRA_MODULES)

CLEANFILES=$(libexec_SCRIPTS)

AM_INSTALL_PROGRAM_FLAGS=@INSTALL_OPTS@

.pm :
	$(AWK) -f ./subst $< > $@
	chmod +x $@

.pl :
	$(AWK) -f ./subst $< > $@
	chmod +x $@

.sh :
	$(AWK) -f ./subst $< > $@
	chmod +x $@

$(libexec_SCRIPTS) : $(EXTRA_DIST)
	$(ECHO) "#! #PERL# -w" | $(AWK) -f ./subst > $@
	$(ECHO) "# nagios: -epn" >> $@
	$(ECHO) >> $@
	$(ECHO) "my %ERRORS=( OK => 0, WARNING => 1, CRITICAL => 2, UNKNOWN => 3 );" >> $@
	$(ECHO) "my %ERRORCODES=( 0 => 'OK', 1 => 'WARNING', 2 => 'CRITICAL', 3 => 'UNKNOWN' );" >> $@
	for m in ${EXTRA_MODULES}; do \
		$(SED) -e 's/^1;//g' < $$m | $(AWK) -f ./subst | $(GREP) -v "my %ERROR" >> $@; \
	done
	if [ -d "${MYMODULES_DIR}" ]; then \
		for m in ${MYMODULES_DIR}/CheckOracleHealthExt*.pm; do \
			if [ -f $$m ]; then \
				$(ECHO) found $$m; \
				$(SED) -e 's/^1;//g' < $$m | $(AWK) -f ./subst | $(GREP) -v "my %ERROR" >> $@; \
			fi \
		done \
	fi
	$(CAT) check_oracle_health.pl | $(GREP) -v "^use Nagios" | $(GREP) -v "^my %ERROR" | $(AWK) -f ./subst >> $@
	chmod +x $@
