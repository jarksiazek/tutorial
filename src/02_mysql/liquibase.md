# LIQUIBASE #

* update value where value is null
```xml
<changeSet author="jksiazek" id="changelog-4.1">
    <update tableName="statement_of_work_snapshots">
        <column name="statement_of_work_completion_edited" valueNumeric="0"/>
        <where>statement_of_work_completion_edited IS NULL</where>
    </update>
</changeSet>
```

* add not null constraint
```xml
<changeSet author="jksiazek" id="changelog-4.1">
    <addNotNullConstraint tableName="statement_of_work_snapshots"
        columnName="your_business_edited" columnDataType="tinyint(1)"/>
</changeSet>
```