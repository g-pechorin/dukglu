cmake_minimum_required(VERSION 3.1.0)

project(dukglue)
get_filename_component(FIPS_ROOT_DIR "../fips" ABSOLUTE)
include("${FIPS_ROOT_DIR}/cmake/fips.cmake")

fips_setup()

	fips_begin_module(dukglu)
		fips_dir(include)
		fips_files(
			# fake source file
			dukglu.cpp

			dukglue/detail_class_proto.h
			dukglue/detail_constructor.h
			dukglue/detail_function.h
			dukglue/detail_method.h
			dukglue/detail_primitive_types.h
			dukglue/detail_refs.h
			dukglue/detail_stack.h
			dukglue/detail_traits.h
			dukglue/detail_typeinfo.h
			dukglue/detail_types.h
			dukglue/dukexception.h
			dukglue/dukglue.h
			dukglue/dukvalue.h
			dukglue/public_util.h
			dukglue/register_class.h
			dukglue/register_function.h
			dukglue/register_property.h
		)
	fips_end_module()
	target_include_directories(dukglu PUBLIC include)


	fips_begin_app(dukglue_test cmdline)
		fips_deps(dukglu)
		fips_deps(duktape)
		fips_dir(tests)
		fips_files(
			main.cpp
			test_assert.cpp
			test_classes.cpp
			test_inheritance.cpp
			test_multiple_contexts.cpp
			test_primitives.cpp
			test_properties.cpp
			test_dukvalue.cpp
		)
	fips_end_app()
	target_compile_features(dukglue_test PRIVATE cxx_variadic_templates cxx_auto_type)

fips_finish()