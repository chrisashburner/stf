# stf
using simple features geometry for temporal data manipulation

I think this might work...

suppose we have data that can be represented along spans of time, e.g. 

table_a <- tibble::tribble(
  ~Group,       ~start,         ~end,
  "a",     "1/01/2023", "16/01/2023",
  "a",    "16/01/2023", "11/02/2023",
  "a",    "11/02/2023",  "9/03/2023",
  "a",     "9/03/2023", "13/04/2023",
  "b",    "13/04/2023", "28/05/2023",
  "b",    "28/05/2023", "21/06/2023",
  "b",    "21/06/2023",  "8/08/2023",
  "b",     "8/08/2023", "16/09/2023",
  "b",    "16/09/2023",  "3/11/2023",
  "b",     "3/11/2023",  "23/12/2023"
)

we can represent these are geometry primitives, as below

table_a$start <- lubridate::dmy(table_a$start)
table_a$end <- lubridate::dmy(table_a$end)
table_a$geom <- paste0("LINESTRING(", as.numeric(table_a$start), " 0, ", as.numeric(table_a$end), " 0)")

then we can use the sf package or something similiar to manipulate these data structures.

sf_a = st_as_sf(table_a, wkt = "geom")


For example:

1. 
