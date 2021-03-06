AM_CPPFLAGS= -fPIC -I${top_srcdir}/src \
	    -I$(TBLIB_ROOT)/include/tbsys \
	    -I$(TBLIB_ROOT)/include/tbnet \
	    -I${top_srcdir}/src/storage/fdb \
	    -I${top_srcdir}/src/storage/mdb \
            -I${top_srcdir}/src/common \
	    -I${top_srcdir}/src/storage/ \
            -I${top_srcdir}/src/packets \
            -I${top_srcdir}/src/dataserver \
            -I${top_srcdir}/src/statserver/include \
	    -I${top_srcdir}/src/plugin \
	    ${BOOST_CPPFLAGS}

LDADD=$(TBLIB_ROOT)/lib/libtbnet.a \
      $(TBLIB_ROOT)/lib/libtbsys.a

multi_cluster_impl_source=tair_multi_cluster_client_impl.hpp tair_multi_cluster_client_impl.cpp \
			  cluster_handler_manager.hpp cluster_handler_manager.cpp \
			  cluster_info_updater.hpp cluster_info_updater.cpp

api_source_list=tair_client_api.cpp i_tair_client_impl.hpp i_tair_client_impl.cpp tair_client_api_impl.cpp \
		${top_srcdir}/src/packets/packet_factory.cpp \
		${top_srcdir}/src/packets/packet_streamer.cpp \
		${top_srcdir}/src/common/data_entry.cpp \
		tair_client_capi.hpp tair_client_api.hpp \
	       	tair_client_api_impl.hpp tair_client_capi.hpp \
          local_cache.hpp local_cache.hpp \
          string_local_cache.h string_local_cache.cpp \
          data_entry_local_cache.h data_entry_local_cache.cpp \
		tair_client.hpp ${multi_cluster_impl_source}

if WITH_READLINE
READLINE_LDFLAGS= -lreadline -ltermcap
endif

if WITH_COMPRESS
COMPRESS_LDFLAGS= -lsnappy
endif

AM_LDFLAGS=-lpthread -lz -lrt ${BOOST_LDFLAGS} @BOOST_THREAD_LIB@  ${GCOV_LIB} ${READLINE_LDFLAGS} ${COMPRESS_LDFLAGS}

lib_LTLIBRARIES=libtairclientapi.la libtairclientapi_c.la libtairclientapi_impl.la
sbin_PROGRAMS=tairclient keycleantool

tairclient_SOURCES=tair_client.cpp
tairclient_LDADD=libtairclientapi.la  ${LDADD}
tairclient_LDFLAGS= -static

keycleantool_SOURCES=tair_key_clean.cpp del_job.hpp nonblock_queue.hpp clean_worker.hpp config_loader.hpp
keycleantool_LDADD=libtairclientapi.la ${LDADD}
keycleantool_LDFLAGS= -static

libtairclientapi_la_SOURCES=${api_source_list}
libtairclientapi_impl_la_SOURCES=${api_source_list}
libtairclientapi_c_la_SOURCES=tair_client_capi.cpp
libtairclientapi_c_la_LIBADD=libtairclientapi.la

include_HEADERS=tair_client_api.hpp tair_client_capi.hpp local_cache.h local_cache.hpp data_entry_local_cache.h
