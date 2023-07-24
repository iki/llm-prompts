Convert the MySQL input to Prisma schema while following the output rules and sample output format.

# Output Rules

- remove comments
- for each table use PascalCase model name and add `@@map(<tableName>)` as a last line of the model block
- for each table with auto increment specified, add `ac:<start>` comment at the auto-incremented field line
- for each table with specified charset, add `cs:<charset>` comment as a last line of the model block
- for each field use camelCase field name and add @map(<fieldName>) directive
- for each varchar field with specified length use `@db.VarChar(<length>)` directive
- for each decimal field with specified precision use `@db.Decimal(<precision>, <scale>)` directive
- for each tinyint field use `@db.TinyInt()` without width
- for each int or tinyint field with specified width add `w:<width>` comment
- for each field with specified charset that is different from current model charset, add `cs:<charset>` comment
- for each field put the directives in order: `@id`, `@unique`, `@db.*`, `@default`, `@map`

# Sample Input

```sql
--
-- Table structure for table `Sample_Data`
--

DROP TABLE IF EXISTS `Sample_Data`;
CREATE TABLE `Sample_Data` (
  `ID` int(10) unsigned NOT NULL auto_increment,
  `Label` varchar(150) NOT NULL,
  `Street` varchar(70),
  `Code` varchar(10) character set latin2 NOT NULL,
  `id_Other` int(10) unsigned default NULL,
  `Flag` tinyint(4) default '0',
  `Number_X` decimal(19,4) default NULL,
PRIMARY KEY (`id`)
) AUTO_INCREMENT=13145 DEFAULT CHARSET=cp1252;
```

# Sample Output

```prisma
model SampleData {
  id      Int      @id @default(autoincrement()) @map("ID") // ai:13145 w:10
  label   String   @db.VarChar(150) @map("Label")
  street  String?  @db.VarChar(70) @map("Street")
  code    String   @db.VarChar(10) @map("Code") // cs:latin2
  idOther Int?     @map("id_Other") // w:10
  flag    Int      @db.TinyInt() @default(0) @map("Flag") // w:4
  numberX Decimal? @db.Decimal(19, 4) @map("Number_X")

  @@map("sample_Data") // cs:cp1252
}
```

# MySQL Input

```sql

```
