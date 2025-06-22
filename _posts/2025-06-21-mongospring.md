---
title: MongoDB - SpringBoot / "_class" 필드 제거 
date: 2025-06-21 15:39 +000
categories: [Database, MongoDB, SpringBoot]
tags: [Kafka]
---

> [Spring Data MongoDB - Type Mapping](https://docs.spring.io/spring-data/mongodb/reference/mongodb/converters-type-mapping.html)
{: .prompt-info}


## `_class` 필드 

- Spring Data MongoD를 별다른 설정없이 사용하면 컬렉션에 객체를 저장할 때, 자동으로 객체의 Java 클래스 이름을 포함하고 있는 `_class` 라는 필드가 추가되어 저장됨
- 역직렬화 정확성 확보 : 데이터를 조회할 때 다시 해당 클래스의 인스턴스로 역직렬화(deserialization) 하는데 사용됨
- 다형성 지원 

```mongodb-json
{
  "_id": ObjectId("..."),
  "name": "Alice",
  "_class": "com.example.User"
}
```

## `_class` 필드 제외하고 저장하는 방법 

```java
@Bean
public MappingMongoConverter mappingMongoConverter(
    MongoDatabaseFactory mongoDatabaseFactory,
    MongoMappingContext mongoMappingContext
) {
  DbRefResolver dbRefResolver = new DefaultDbRefResolver(mongoDatabaseFactory);
  MappingMongoConverter converter = new MappingMongoConverter(dbRefResolver, mongoMappingContext);
  converter.setTypeMapper(new DefaultMongoTypeMapper(null));
  return converter;
}
```


