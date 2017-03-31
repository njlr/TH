def merge_dicts(x, y):
  z = x.copy()
  z.update(y)
  return z

genrule(
  name = 'cmake',
  out = 'out',
  srcs = glob([
    '*.h',
    '*.c',
    '*.in',
    '*.md',
    '*.txt',
    'cmake/*.cmake',
  ]),
  cmd = 'mkdir -p $OUT && cd $OUT && cmake $SRCDIR',
)

genrule(
  name = 'THGeneral.h',
  out = 'THGeneral.h',
  cmd = 'cp $(location :cmake)/THGeneral.h $OUT ',
)

cxx_library(
  name = 'th',
  header_namespace = '',
  exported_headers = merge_dicts(subdir_glob([
    ('', '*.h'),
  ]), {
    'THGeneral.h': ':THGeneral.h',
  }),
  srcs = glob([
    '*.c',
  ]),
  visibility = [
    'PUBLIC',
  ],
)
