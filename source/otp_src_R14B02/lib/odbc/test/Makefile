#
# %CopyrightBegin% 
# 
# Copyright Ericsson AB 1999-2011. All Rights Reserved.
# 
# The contents of this file are subject to the Erlang Public License,
# Version 1.1, (the "License"); you may not use this file except in
# compliance with the License. You should have received a copy of the
# Erlang Public License along with this software. If not, it can be
# retrieved online at http://www.erlang.org/.
# 
# Software distributed under the License is distributed on an "AS IS"
# basis, WITHOUT WARRANTY OF ANY KIND, either express or implied. See
# the License for the specific language governing rights and limitations
# under the License.
# 
# %CopyrightEnd%
#
include $(ERL_TOP)/make/target.mk
include $(ERL_TOP)/make/$(TARGET)/otp.mk


INCLUDES= -I. -I$(ERL_TOP)/lib/test_server/include/  -I$(ERL_TOP)/lib/odbc/src

# ----------------------------------------------------
# Target Specs
# ----------------------------------------------------

MODULES= \
	odbc_start_SUITE \
	odbc_connect_SUITE \
	odbc_query_SUITE \
	odbc_data_type_SUITE \
	odbc_test_lib \
	oracle \
	sqlserver \
	postgres

EBIN = .

ERL_FILES= $(MODULES:%=%.erl)

HRL_FILES= odbc_test.hrl\

TARGET_FILES= \
	$(MODULES:%=$(EBIN)/%.$(EMULATOR))

SPEC_FILES = odbc.spec
COVER_FILE = odbc.cover

EMAKEFILE  = Emakefile
MAKE_EMAKE = $(wildcard $(ERL_TOP)/make/make_emakefile)

ifeq ($(MAKE_EMAKE),)
BUILDTARGET   = $(TARGET_FILES)
RELTEST_FILES = $(SPEC_FILES) $(SOURCE)
else
BUILDTARGET   = emakebuild
RELTEST_FILES = $(EMAKEFILE) $(SPEC_FILES) $(SOURCE)
endif

# ----------------------------------------------------
# Release directory specification
# ----------------------------------------------------
RELSYSDIR = $(RELEASE_PATH)/odbc_test

# ----------------------------------------------------
# FLAGS
# ----------------------------------------------------

ERL_COMPILE_FLAGS += $(INCLUDES) \

# ----------------------------------------------------
# Targets
# ----------------------------------------------------

tests debug opt: $(BUILDTARGET)

targets: $(TARGET_FILES)

.PHONY: emakebuild

emakebuild: $(EMAKEFILE)

$(EMAKEFILE): 
	$(MAKE_EMAKE) $(ERL_COMPILE_FLAGS) -o$(EBIN) '*_SUITE_make' | grep -v Warning > $(EMAKEFILE)
	$(MAKE_EMAKE) $(ERL_COMPILE_FLAGS) -o$(EBIN) $(MODULES) | grep -v Warning >> $(EMAKEFILE)

clean:
	rm -f $(TARGET_FILES)
	rm -f core

docs:

# ----------------------------------------------------
# Release Target
# ---------------------------------------------------- 
include $(ERL_TOP)/make/otp_release_targets.mk

release_spec: opt

release_tests_spec: opt
	$(INSTALL_DIR) $(RELSYSDIR)
	$(INSTALL_DATA) $(SPEC_FILES) $(COVER_FILE) $(ERL_FILES) $(HRL_FILES) $(RELSYSDIR)


release_docs_spec:







