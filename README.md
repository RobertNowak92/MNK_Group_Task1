# MNK_Group_Task1
by Robert Nowak

MNK_Group_Task1_QUERIES.txt contains complete script of the database<br>
MNK_Group_Task1_postgresql contains database with loaded data<br>
Robert_Nowak_task1.csv is created by query below.

Task 1 query:

COPY (<br>
SELECT d.main_part_number, d.manufacturer, d.category, d.origin, p.price,<br>
coalesce(de.deposit, 0) AS deposit,<br>
p.price + coalesce(de.deposit, 0) AS final_price,<br>
replace(q.quantity, '>', '')::INT AS quantity FROM data d<br>
INNER JOIN price p ON p.part_number = d.part_number<br>
INNER JOIN quantity q ON q.part_number = d.part_number<br>
LEFT JOIN deposit de ON de.part_number = d.part_number<br>
WHERE <br>
(q.warehouse LIKE 'A' <br>
OR q.warehouse LIKE 'H'<br>
OR q.warehouse LIKE 'J'<br>
OR q.warehouse LIKE '3'<br>
OR q.warehouse LIKE '9')<br>
AND replace(q.quantity, '>', '')::INT != 0<br>
AND p.price + coalesce(de.deposit, 0) > 2.00<br>
    )<br>
TO 'C:\Users\robno\Documents\Github_proj\MNK_Group_Task1\Robert_Nowak_task1.csv'<br>
DELIMITER ';'<br>
CSV HEADER;

