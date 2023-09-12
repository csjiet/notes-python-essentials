Resources:
- [Parquet files](https://towardsdatascience.com/demystifying-the-parquet-file-format-13adb0206705)

Generic file type
1. gzip
	1. extension: `.gz`
2. zip
3. bz2
4. zstd
5. tar

Specific file type
1. csv
	1. extension: `.csv` 
	2. write: `df.to_csv('file_name.csv', index=False)`
		1. Arguments:
			1. `path` : IMPLIED
			2. `index=False`: So that it does not create a new 'index' column in the csv file.
			3. `compression= {file_type}`:
				1. Compressed file type: `zip`, `gzip`, `bz2`, `zstd`, `tar`
			4. `sep = {}`
			5. `na_rep = {}`
			6. `float_format = {}`
			7. `columns = {}`
			8. `header = {}`
			9. `index_label = {}`
			10. `mode = {}`
			11. `encoding = {}`
			12. `quoting = {}`
			13. `quotechar = {}`
			14. `lineterminator = {}` 
			15. `chunksize = {}`
			16. `data_format = {}`
			17. `doublequote = {}`
			18. `escapechar = {}`
			19. `decimal = {}`
			20. `errors = {}`
			21. `storage_options = {}`
	3. read: `df = pd.read_csv('file_name.csv', index_col= [0], dtype={'col_1': 'pandas_dtype','col_2': 'pandas_dtype', ...})`
		1. Arguments:
			1. `index_col=[0]`: Eliminate the index column (if the csv has one) when reading into a data frame.
			2. `dtype={'col_1': 'pandas_dtype', ...}`: Preset each columns data type when data is being read. 
	4. Benefits:
		1. Pervasive usage 
		2. Easily readable in any text editor
	5. Cons:
		1. dtypes (data types) in Pandas DataFrame are not retained after writing, and will not recognized after being read.
2. pickle
	1. extension: `.pkl` 
	2. write:  `df.to_pickle('file_name.pkl')`
		1. Arguments:
			1. `path` : IMPLIED
			2. `compression= {file_type}` : 
				1. Compressed file type: `zip`, `gzip`, `bz2`, `zstd`, `tar`
			3. `protocol={0-5}`:
			4. `storage_options ={}`
	3. read: `df = pf.read_pickle('file_name.pkl')` 
		1. Arguments:
			1. 
	4. Benefits:
		1. dtypes are retained when written, and read.
	5. Cons:
		1. Large memory usage (BUT smaller than: csv)
	1. extension: `.parquet` 
	2. Installation:
		1. `!pip install pyarrow` OR 
		3. `!pip install fastparquet`
	3. write: `df.to_parquet('file_name.extension',compression= '' )`
		1. Arguments:
			1. `path` : IMPLIED
			2. `compression = {file_type}`: 
				1. Compressed file type: `snappy` (default), `gzip`, `brotli`, `None`, 
			3. `engine = {}`
			4. `index = {}`
			5. `partition_cols = {}`
			6. `storage_options = {}`
	4. read: `df = pd.read_parquet('file_name.extension', columns = ['col_1', 'col2'])`
		1. Arguments:
			1. `columns=['col_1', 'col_2', ...]`: Reading specific columns that we read into the data frame.
	5. Benefits:
		1. dtypes are retained when written, and read.
		2. Small memory usage  (Best)
		3. Faster writes 
		4. Faster reads 
	6. Cons:
4. Feather
	- extension: `.feather`
	1. Installation:
		1. `!pip install pyarrow` OR 
		3. `!pip install fastparquet`
	2. write: `df.to_feather('file_name.extension')`
		1. Arguments:
			1. `path`: IMPLIED
			2. `dest = {}` 
			3. `compression = {file_type}` :
				1. Compressed file type: `None` (default), `zstd`, `lz4`, `uncompressed` 
			4. `compression_level = {}`:
			5. `chunksize = {}`:
			6. `version = {}`:
	3. read: `df = pd.read_feather('file_name.extension')`
	4. Benefits:
		1. dtypes are retained when written, and read.
		2. Fast read  (faster than: pickle, csv)
		3. Fast write (faster than: pickle, csv)
		4. Small memory usage
	5. Cons:
6. Jay
	- extension: `.jay` 
	1. write: `df.to_jay('file_name.extension')`
	2. read: ``


Other:
1. orc
2. hdf
3. sql
4. dict
5. excel
6. json
7. html
8. latex
9. stata
10. gbq
11. records
12. string
13. clipboard
14. markdown

Resources: 
- https://www.youtube.com/watch?v=u4rsA5ZiTls