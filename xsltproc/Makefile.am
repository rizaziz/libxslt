AM_CPPFLAGS = -I$(top_srcdir) -I$(top_srcdir)/libxslt -I$(top_srcdir)/libexslt \
	      -I$(top_builddir) -I$(top_builddir)/libxslt \
	      -I$(top_builddir)/libexslt

EXTRA_PROGRAMS=
bin_PROGRAMS = xsltproc

noinst_PROGRAMS=testThreads

AM_CFLAGS = $(LIBGCRYPT_CFLAGS) $(LIBXML_CFLAGS) $(LIBXSLT_CFLAGS)

xsltproc_SOURCES = xsltproc.c
xsltproc_LDFLAGS = 
xsltproc_DEPENDENCIES = $(DEPS)

testThreads_SOURCES=testThreads.c
testThreads_LDFLAGS =
testThreads_DEPENDENCIES = $(DEPS)
testThreads_LDADD=  $(THREAD_LIBS) $(LDADDS)

DEPS = $(top_builddir)/libxslt/libxslt.la \
	$(top_builddir)/libexslt/libexslt.la 

LDADDS = $(top_builddir)/libxslt/libxslt.la \
         $(top_builddir)/libexslt/libexslt.la \
	$(LIBXML_LIBS) $(EXTRA_LIBS) $(LIBM)

xsltproc_LDADD = $(LDADDS)

CLEANFILES = .memdump

$(top_builddir)/libxslt/libxslt.la:
	cd $(top_builddir)/libxslt && $(MAKE) libxslt.la

$(top_builddir)/libexslt/libexslt.la: $(top_builddir)/libxslt/libxslt.la
	cd $(top_builddir)/libexslt && $(MAKE) libexslt.la

tests: testThreads
	@echo > .memdump
	@echo '## Running testThreads'
	@($(CHECKER) ./testThreads > /dev/null; grep "MORY ALLO" .memdump  | grep -v "MEMORY ALLOCATED : 0" || true)
