nvtxpy
======

Python bindings to nvtx plus some extra support code.

Make it easy to use the add markers for nvvp in Python plus some extra
profiling support code.

Installation
============

Install using

    python setup.py install #Global

The `--user` flag can be used to install only to the user's current directory.



Usage
============



    with nvtxpy.profile_range_nvtx_only(name, color, payload, category) as value:
      #Code

    with nvtxpy.profile_range(name, color, payload, category) as value:
      #Code

      nvtxpy.colors.red
 red, green, blue, yellow, magenta, cyan, white, black,


profile_mark(message, color=None, payload=None, category=None):
profile_range_push(message, color=None, payload=None, category=None):
profile_range_pop


    profiled ???

    getstats()


@nvtxpy.profiled("propagate", category=None, color=None, payload=None)
def propagate( input_field, pixel_size_um, ref_idx, wavelength_nm, z_um,
               tf_input_is_spectrum=False, tf_outputting_spectrum=False,
               transfer_function=None, tf_output_transfer_function=False,
             ):