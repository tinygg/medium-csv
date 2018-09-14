# medium-csv
## feature quick tests

/**
     * author: tinygg
     * @throws IOException
     */
    @Test
    public void testSkipLineNumbers() throws IOException {

        //1. skip line number 1, 3
        //2. allow same column name , and auto rename with {old_repeat_column_name}@2, {old_repeat_column_name}@3, {old_repeat_column_name}@4 ...
        CSVFormat format = CSVFormat.DEFAULT.withFirstRecordAsHeader().withSkipLines(1L, 3L).withAllowSameName(true, "@");
        format = format.withAllowMissingColumnNames(true);
        format = format.withSkipHeaderRecord(true);
        format = format.withCommentMarker('#');
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
