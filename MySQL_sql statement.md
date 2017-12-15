------
####  MySQL SQL Statement
##### A. `分组排序 ROW_NUMBER() OVER(PARTITION BY) `
- <b>Example</b>
```SQL
SELECT          *
FROM            (
                    SELECT      A.id_1,
                                A.id_2,
                                A.val,
                                @rownum:=@rownum+1 ,
                                if(@pdept=A.id_1 && @pdept2=A.id_2 ,@rank:=@rank+1,@rank:=1) as rank,
                                @pdept:=A.id_1,
                                @pdept2:=A.id_2

                    FROM (
                            SELECT      *
                            FROM        (
                              SELECT    '1' as id_1,
                                        '1' as id_2,
                                        'ID' as val 
                              UNION ALL
                              SELECT    '1' as id_1,
                                        '1' as id_2,
                                        'OD' as val 
                              UNION ALL
                              SELECT    '2' as id_1,
                                        '1' as id_2,
                                        'OD' as val  
                              UNION ALL
                              SELECT    '2' as id_1,
                                        '2' as id_2,
                                        'ID' as val                                              
                              UNION ALL
                              SELECT    '2' as id_1,
                                        '1' as id_2,
                                        'OD' as val  
                              UNION ALL
                              SELECT    '2' as id_1,
                                        '2' as id_2,
                                        'ID' as val  
                              UNION ALL
                              SELECT    '3' as id_1,
                                        '1' as id_2,
                                        'ID' as val 
                            ) AS XX
                            ORDER BY     id_1 ASC,id_2 ASC,val DESC
                        ) A ,( SELECT    @rownum :=0 , @pdept := NULL ,@pdept2:=NULL,@rank:=0) B 
                ) X
WHERE           rank = 1
;
```
