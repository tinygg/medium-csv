# medium-csv
## feature quick tests

```
    /**
     * author: tinygg ::moji
     * @throws IOException
     */
    @Test
    public void testSkipLineNumbers() throws IOException {

        //1. skip line number 1, 3
        //2. allow same column name , and auto rename with {old_repeat_column_name}@2, {old_repeat_column_name}@3, {old_repeat_column_name}@4 ...
        CSVFormat format = CSVFormat.DEFAULT.withFirstRecordAsHeader()
        .withSkipLines(1L, 3L).withAllowSameName(true, "@") 
        .withAllowMissingColumnNames(true);
        .withSkipHeaderRecord(true);
        .withCommentMarker('#');
        try (final CSVParser parser = format.parse(getTestInput("CSVSkipLines/test_skiplines.csv"))) {
            int lines = 0;
            for (final CSVRecord csvRecord : parser) {
                String line = csvRecord.toString();
                System.out.println(line);
                lines++;
            }
            System.out.println("line count:"+lines);
        }
    }
```

## test data
```
xxxxxxxxxxxxxxxxxxx(skip line one)(1.this is a skip row 2.same column name auto rename, showed next line.)
,,aAILL,aAILL
,,DEG,DEG(skip line two)
52,,0.22,0.22
53,,0.19,0.19
54,,0.22,0.19
55,,0.19,0.19
# this is a comment line start with '#'
56,,0.22,0.28
57,,0.19,0.28
58,,0.19,0.22
```

## output
```
CSVRecord [comment=,DEG,DEG(skip line two), mapping={=1, aAILL=2, aAILL@2=3}, recordNumber=1, values=[52, , 0.22, 0.22]]
CSVRecord [comment=null, mapping={=1, aAILL=2, aAILL@2=3}, recordNumber=2, values=[53, , 0.19, 0.19]]
CSVRecord [comment=null, mapping={=1, aAILL=2, aAILL@2=3}, recordNumber=3, values=[54, , 0.22, 0.19]]
CSVRecord [comment=null, mapping={=1, aAILL=2, aAILL@2=3}, recordNumber=4, values=[55, , 0.19, 0.19]]
CSVRecord [comment=this is a comment line start with '#', mapping={=1, aAILL=2, aAILL@2=3}, recordNumber=5, values=[56, , 0.22, 0.28]]
CSVRecord [comment=null, mapping={=1, aAILL=2, aAILL@2=3}, recordNumber=6, values=[57, , 0.19, 0.28]]
CSVRecord [comment=null, mapping={=1, aAILL=2, aAILL@2=3}, recordNumber=7, values=[58, , 0.19, 0.22]]
line count:7
```

