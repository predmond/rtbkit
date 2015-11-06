add_library(googleurl SHARED
	src/gurl.cc
	src/url_canon_etc.cc
	src/url_parse_file.cc
	src/url_canon_mailtourl.cc
	src/url_canon_icu.cc
	src/url_canon_fileurl.cc
	src/url_canon_pathurl.cc
	src/url_parse.cc
	src/url_canon_host.cc
	src/url_canon_relative.cc
	src/url_canon_ip.cc
	src/url_util.cc
	src/url_canon_filesystemurl.cc
	src/url_canon_internal.cc
	src/url_canon_stdurl.cc
	src/url_canon_path.cc
	src/url_canon_query.cc)
target_link_libraries(googleurl icui18n icuuc icudata m)
add_definitions(-Duint64=uint64_t)
