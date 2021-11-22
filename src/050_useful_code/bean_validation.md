```java
package com.yell.statementofwork.common;

import javax.validation.Validation;
import javax.validation.Validator;
import java.lang.reflect.Field;

import static org.junit.jupiter.api.Assertions.assertEquals;

public class BeanValidationTester {

    private static final Validator validator = Validation.buildDefaultValidatorFactory().getValidator();

    public static <T> void testNumberField(T object, String fieldName, Integer min, Integer max) throws Exception {
        if (max != null) testNumberFieldMax(object, fieldName, max);
        if (min != null) testNumberFieldMin(object, fieldName, min);
    }

    private static <T> void testNumberFieldMax(T object, String fieldName, Integer max) throws Exception {
        //over max
        assertEquals(1, validator.validate(instanceWithSetProperField(object, fieldName, max + 1)).size(), "OVER MAX");
        //max
        assertEquals(0, validator.validate(instanceWithSetProperField(object, fieldName, max)).size(), "MAX");
    }

    private static <T> void testNumberFieldMin(T object, String fieldName, Integer min) throws Exception {
        //min
        assertEquals(0, validator.validate(instanceWithSetProperField(object, fieldName, min)).size(), "MIN");
        //lower min
        assertEquals(1, validator.validate(instanceWithSetProperField(object, fieldName, min - 1)).size(), "LOWER MIX");
    }

    public static <T> void testStringField(T object, String fieldName, int min, int max) throws Exception {
        //over max
        assertEquals(1, validator.validate(instanceWithSetProperField(object, fieldName, "1".repeat(max + 1))).size(), "OVER MAX");
        //max
        assertEquals(0, validator.validate(instanceWithSetProperField(object, fieldName, "1".repeat(max))).size(), "MAX");
        //min
        assertEquals(0, validator.validate(instanceWithSetProperField(object, fieldName, "1".repeat(min))).size(), "MIN");
        //lower min
        if (min > 0)
            assertEquals(1, validator.validate(instanceWithSetProperField(object, fieldName, "1".repeat(min - 1))).size(), "LOWER MIN");
    }

    private static <T> T instanceWithSetProperField(T object, String fieldName, Object value) throws Exception {
        Field field = object.getClass().getDeclaredField(fieldName);
        field.setAccessible(true);
        field.set(object, value);
        return object;
    }
}

```