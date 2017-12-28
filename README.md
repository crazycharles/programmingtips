# Programming tips about Python


## 1.Load a large file
<pre>
with open(filename, 'rb') as f:
	for line in f:
		do something with the line</pre>
## 2.Update all your python's packages
<pre>
import pip
from subprocess import call

for dist in pip.get_installed_distributions():
    call("pip install --upgrade " + dist.project_name, shell=True)</pre>
## 3.How to write or read a csv file
<pre>
import csv
def handlecsv(wantWrite=True, filename='', content=list()):
    if wantWrite:
    # write to a csv file called filename with content
        with open(filename, 'w', newline='') as csvfile:
            filewriter = csv.writer(csvfile)
            for row in content:
                filewriter.writerow(row)
    else:
    # open a csv file called filename
        dataset = list()
        with open(filename, 'r') as csvfile:
            filereader = csv.reader(csvfile)
            for row in filereader:
                dataset.append(row)
        return dataset</pre>

## 4.How to write or read a excel file
<pre>
import xlwt
import xlrd
def handleExcel(wantWrite=True, sheetname='sheet1', sheet_id=0, content=list(), filename=""):
    if wantWrite:
    # write a excel in sheetname with content, and save it with filename
        workbook = xlwt.Workbook()
        sheet1 = workbook.add_sheet(sheetname, cell_overwrite_ok=True)
        for index, i in enumerate(content):
            c = len(i)
            for j in range(c):
                sheet1.write(index, j, i[j])
        workbook.save(filename)
    else:
    # read a excel file called filename, sheet_id is its sheet index
        data = xlrd.open_workbook(filename)
        table = data.sheets()[sheet_id]
        nrows = table.nrows
        excel_values = []
        for i in range(1, nrows):
            excel_values.append(table.row_values(i))
        return excel_values</pre>
## 4.How to sort a list and get the index according to their values

<pre>
def getLargeValueIndex(a = list()):
    a_dict = {}
    for index, i in enumerate(a):
        a_dict[index] = i
    return sorted(a_dict, key=a_dict.get, reverse=True)</pre>
<pre>Examples:
input [1,3,2,6]
output {'3':6,'1':3,'2':2,'0':1}</pre>

## Reference
1.<href>https://stackoverflow.com/questions/8009882/how-to-read-large-file-line-by-line-in-python</href>
