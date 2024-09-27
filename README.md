#EditREADME
# Thank you for visiting my page
Welcome to my Immigration, Refugees and Citizenship Canada (IRCC) Forecasting and Dashboard. Where I utilized open source immigration data from the government of Canada to both forecast immigration and built a dashboard to more easily explore the data. Kindly note that Immigration Canada has deemed that countries with 2-5 immigrants have a denomination of 0 in the raw data

## How to set up files
1. To set up files download the raw csv files from here or find online at https://open.canada.ca/data/en/dataset/9b34e712-513f-44e9-babf-9df4f7256550 into a folder
2. Either open the ##IRCC Data Forecast## to view forecasting in an Excel file or ##IRCC Tableau Raw Fil$$ to see find steps on how data was cleaned
3. Click on the Data Tab -> Get Data -> Data Source Settings -> Change Source and then the folder in whicn you downloaded the raw csv
4. From there you should have full access to the data
5. If you want to see how the data was cleaned and formatted to make it easier to read
6. Click on the Data Tab -> Get Data -> Launch Power Query Editor -> Look at the right panel and read/click on the gears to see the steps taken

## Looking at the data in Tableau
Please find the links to my Tablea Dashboards below to easily explore the data
1. https://public.tableau.com/app/profile/cam5684/viz/IRCCGeneralDashboard/GeneralDashboard (General Info Dashboard)

## Steps taken to clean the data with only Raw CSV files (Requires Excel 2019)
1. Go to data tab in excel -> Get Data -> From Folder -> Click on folder storing Raw CSV -> click on Combine + Transform Data (Will automatically open PowerQuery)
2. In Advanced Editor on Home Tab
let
    Source = Folder.Files("C:\Users\Cam\Desktop\IRCC CSV - Copy\Country of Citizenship"),
    #"Filtered Hidden Files1" = Table.SelectRows(Source, each [Attributes]?[Hidden]? <> true),
    #"Invoke Custom Function1" = Table.AddColumn(#"Filtered Hidden Files1", "Transform File", each #"Transform File"([Content])),
    #"Renamed Columns1" = Table.RenameColumns(#"Invoke Custom Function1", {"Name", "Source.Name"}),
    #"Removed Other Columns1" = Table.SelectColumns(#"Renamed Columns1", {"Source.Name", "Transform File"}),
    #"Expanded Table Column1" = Table.ExpandTableColumn(#"Removed Other Columns1", "Transform File", Table.ColumnNames(#"Transform File"(#"Sample File"))),
    #"Changed Type" = Table.TransformColumnTypes(#"Expanded Table Column1",{{"Source.Name", type text}, {"EN_YEAR", Int64.Type}, {"EN_QUARTER", type text}, {"EN_MONTH", type text}, {"FR_ANNEÃ‰", Int64.Type}, {"FR_TRIMESTRE", type text}, {"FR_MOIS", type text}, {"EN_COUNTRY_OF_CITIZENSHIP", type text}, {"FR_PAYS_DE_CITOYENNETÃ‰", type text}, {"TOTAL", type text}}),
    #"Advanced Editor Country Rename" = Table.ReplaceValue(#"Changed Type", each [EN_COUNTRY_OF_CITIZENSHIP], each 
if Text.Contains([EN_COUNTRY_OF_CITIZENSHIP], "Aland Island") then "Aland Islands" else
if Text.Contains([EN_COUNTRY_OF_CITIZENSHIP], "Bahama Islands, The") then "Bahamas" else
if Text.Contains([EN_COUNTRY_OF_CITIZENSHIP], "Benin, Republic of") then "Benin" else
if Text.Contains([EN_COUNTRY_OF_CITIZENSHIP], "Bonaire, Sin Eustatius And Saba") then "Bonaire, Sint Eustatius And Saba" else  
if Text.Contains([EN_COUNTRY_OF_CITIZENSHIP], "Botswana, Republic of") then "Botswana" else 
if Text.Contains([EN_COUNTRY_OF_CITIZENSHIP], "Cameroon, Federal Republic of") then "Cameroon" else
if Text.Contains([EN_COUNTRY_OF_CITIZENSHIP], "Chad, Republic of") then "Chad" else
if Text.Contains([EN_COUNTRY_OF_CITIZENSHIP], "China, People's Republic of") then "China" else
if Text.Contains([EN_COUNTRY_OF_CITIZENSHIP], "Congo, People's Republic of") then "Congo" else 
if Text.Contains([EN_COUNTRY_OF_CITIZENSHIP], "Congo, Democratic Republic of") then "Democratic Republic of Congo" else
if Text.Contains([EN_COUNTRY_OF_CITIZENSHIP], "Djibouti, Republic of") then "Djibouti" else
if Text.Contains([EN_COUNTRY_OF_CITIZENSHIP], "East Timor, Democratic Republic of") then "Timor Leste" else
if Text.Contains([EN_COUNTRY_OF_CITIZENSHIP], "Equatorial Guinea, Republic of") then "Equatorial Guinea" else
if Text.Contains([EN_COUNTRY_OF_CITIZENSHIP], "Gabon Republic") then "Gabon" else
if Text.Contains([EN_COUNTRY_OF_CITIZENSHIP], "Guinea, Republic of") then "Guinea" else
if Text.Contains([EN_COUNTRY_OF_CITIZENSHIP], "Hong Kong SAR") then "Hong Kong" else
if Text.Contains([EN_COUNTRY_OF_CITIZENSHIP], "Indonesia, Republic of") then "Indonesia" else
if Text.Contains([EN_COUNTRY_OF_CITIZENSHIP], "Ireland, Republic of") then "Ireland" else
if Text.Contains([EN_COUNTRY_OF_CITIZENSHIP], "Ivory Coast, Republic of") then "Ivory Coast" else
if Text.Contains([EN_COUNTRY_OF_CITIZENSHIP], "Korea, People's Democratic Republic of") then "North Korea" else
if Text.Contains([EN_COUNTRY_OF_CITIZENSHIP], "Korea, Republic of") then "South Korea" else
if Text.Contains([EN_COUNTRY_OF_CITIZENSHIP], "Kosovo, Republic of") then "Kosovo" else
if Text.Contains([EN_COUNTRY_OF_CITIZENSHIP], "Macau SAR") then "Macau" else
if Text.Contains([EN_COUNTRY_OF_CITIZENSHIP], "Maldives, Republic of") then "Maldives" else
if Text.Contains([EN_COUNTRY_OF_CITIZENSHIP], "Mali, Republic of") then "Mali" else
if Text.Contains([EN_COUNTRY_OF_CITIZENSHIP], "Marshall Islands, Republic of the") then "Marshall Islands" else
if Text.Contains([EN_COUNTRY_OF_CITIZENSHIP], "Mongolia, People's Republic of") then "Mongolia" else
if Text.Contains([EN_COUNTRY_OF_CITIZENSHIP], "Montenegro, Republic of") then "Montenegro" else
if Text.Contains([EN_COUNTRY_OF_CITIZENSHIP], "Netherlands, The") then "Netherlands" else
if Text.Contains([EN_COUNTRY_OF_CITIZENSHIP], "Netherlands Antilles, The") then "Netherlands" else
if Text.Contains([EN_COUNTRY_OF_CITIZENSHIP], "Nevis") then "Saint Kitts and Nevis" else
if Text.Contains([EN_COUNTRY_OF_CITIZENSHIP], "Niger, Republic of the") then "Niger" else
if Text.Contains([EN_COUNTRY_OF_CITIZENSHIP], "Northern Mariana Islands, Commonwealth of the") then "Northern Mariana Islands" else
if Text.Contains([EN_COUNTRY_OF_CITIZENSHIP], "Palestinian Authority (Gaza/West Bank)") then "Palestinian Territories" else
if Text.Contains([EN_COUNTRY_OF_CITIZENSHIP], "Panama, Republic of") then "Panama" else
if Text.Contains([EN_COUNTRY_OF_CITIZENSHIP], "Samoa, Independent State of") then "Samoa" else
if Text.Contains([EN_COUNTRY_OF_CITIZENSHIP], "Serbia, Republic of") then "Serbia" else
if Text.Contains([EN_COUNTRY_OF_CITIZENSHIP], "Somalia, Democratic Republic of") then "Somalia" else
if Text.Contains([EN_COUNTRY_OF_CITIZENSHIP], "South Africa, Republic of") then "South Africa" else
if Text.Contains([EN_COUNTRY_OF_CITIZENSHIP], "South Sudan, Republic of") then "South Sudan" else
if Text.Contains([EN_COUNTRY_OF_CITIZENSHIP], "Sudan, Democratic Republic of") then "Sudan" else
if Text.Contains([EN_COUNTRY_OF_CITIZENSHIP], "Tanzania, United Republic of") then "Tanzania" else
if Text.Contains([EN_COUNTRY_OF_CITIZENSHIP], "Togo, Republic of") then "Togo" else
if Text.Contains([EN_COUNTRY_OF_CITIZENSHIP], "Trinidad and Tobago, Republic of") then "Trinidad and Tobago" else
if Text.Contains([EN_COUNTRY_OF_CITIZENSHIP], "United Kingdom and Overseas Territories") then "United Kingdom" else
[EN_COUNTRY_OF_CITIZENSHIP], Replacer.ReplaceText, {"EN_COUNTRY_OF_CITIZENSHIP"}),
    #"Removed French Columns" = Table.RemoveColumns(#"Advanced Editor Country Rename",{"FR_ANNEÃ‰", "FR_TRIMESTRE", "FR_MOIS", "FR_PAYS_DE_CITOYENNETÃ‰"}),
    #"Replace -- with 0" = Table.ReplaceValue(#"Removed French Columns","--","0",Replacer.ReplaceText,{"TOTAL"}),
    #"Change Data Type Totals" = Table.TransformColumnTypes(#"Replace -- with 0",{{"TOTAL", Int64.Type}}),
    #"Source Name Change PR" = Table.ReplaceValue(#"Change Data Type Totals","ODP-PR-Citz.csv","PR",Replacer.ReplaceText,{"Source.Name"}),
    #"Source Name Change IS" = Table.ReplaceValue(#"Source Name Change PR","ODP-TR-Study-IS_CITZ.csv","IS",Replacer.ReplaceText,{"Source.Name"}),
    #"Source Name Change IMP" = Table.ReplaceValue(#"Source Name Change IS","ODP-TR-Work-IMP-CITZ.csv","IMP",Replacer.ReplaceText,{"Source.Name"}),
    #"Source Name Change TFW" = Table.ReplaceValue(#"Source Name Change IMP","ODP-TR-Work-TFWP-CITZ.csv","TFW",Replacer.ReplaceText,{"Source.Name"}),
    #"Duplicated Column Year" = Table.DuplicateColumn(#"Source Name Change TFW", "EN_YEAR", "EN_YEAR - Copy"),
    #"Duplicated Column Month" = Table.DuplicateColumn(#"Duplicated Column Year", "EN_MONTH", "EN_MONTH - Copy"),
    #"Merged Columns Year/Month" = Table.CombineColumns(Table.TransformColumnTypes(#"Duplicated Column Month", {{"EN_YEAR - Copy", type text}}, "en-CA"),{"EN_YEAR - Copy", "EN_MONTH - Copy"},Combiner.CombineTextByDelimiter(",", QuoteStyle.None),"Date"),
    #"Change ""Date"" to Date Data Type" = Table.TransformColumnTypes(#"Merged Columns Year/Month",{{"Date", type date}}),
    #"Filtered Rows" = Table.SelectRows(#"Change ""Date"" to Date Data Type", each ([Source.Name] = "IMP" or [Source.Name] = "IS" or [Source.Name] = "PR" or [Source.Name] = "TFW"))
in
    #"Filtered Rows"

3. Without coding you can click on columns and edit manually
4. Removed French Columns
5. Replace Nulls with "0" for mathmatical purposes
6. Change Data Types of Totals to "0"
7. Changed Source Name Values to appropriate names
8. Created Date Tab -> Duplicated Year and Month Columns -> Merged Columns -> Separated by Columns -> Change Data data type to "Date" -> Filtered Rows


