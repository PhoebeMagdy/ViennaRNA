AUTOMAKE_OPTIONS = subdir-objects

xxd_verbose = $(xxd_verbose_@AM_V@)
xxd_verbose_ = $(xxd_verbose_@AM_DEFAULT_V@)
xxd_verbose_0 = @echo "  XXD      $@";

SUFFIXES = .ps .hex

TEMPLATE_HEADER_FILES = \
    templates_postscript.h


POSTSCRIPT_FILES = $(PS_TEMPLATE_FILES)


##  Note that we only (re-)build .hex files for direct inclusion into our
##  library if the user has the xxd tool installed. Otherwise, any changes
##  to the postscript templates will NOT propagate into the binary files

if VRNA_AM_SWITCH_HAS_XXD

## The rule for generating .hex files from .ps
.ps.hex:
	$(xxd_verbose)$(XXD) -i < $< > $@ && echo ',0x00' >> $@

templates_postscript.h: $(PS_TEMPLATE_FILES_HEX)

endif


BUILT_SOURCES = \
    $(PS_TEMPLATE_FILES_HEX)


EXTRA_DIST = \
    ps_templates.txt \
    $(TEMPLATE_HEADER_FILES) \
    $(POSTSCRIPT_FILES) \
    ${BUILT_SOURCES}


maintainer-clean-local:
	rm -rf $(BUILT_SOURCES)
