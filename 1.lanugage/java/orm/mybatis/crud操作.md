. CRUD 操作：

- 熟悉 MyBatis 提供的增、删、改、查等基本数据库操作。

  - MyBatis 提供了一些常用的 XML 标签来实现基本的数据库操作，包括增加（插入）、删除、更新和查询等操作。以下是这些操作的示例：

    **1. 插入数据（增加）：**

    ```xml
    <insert id="insertUser" parameterType="com.example.User">
        INSERT INTO users (user_name, user_email)
        VALUES (#{username}, #{email})
    </insert>
    ```

    **2. 更新数据：**

    ```xml
    <update id="updateUser" parameterType="com.example.User">
        UPDATE users
        SET user_name = #{username}, user_email = #{email}
        WHERE user_id = #{id}
    </update>
    ```

    **3. 删除数据：**

    ```xml
    <delete id="deleteUserById" parameterType="Long">
        DELETE FROM users
        WHERE user_id = #{id}
    </delete>
    ```

    **4. 查询数据：**

    ```xml
    <select id="getUserById" resultMap="UserResultMap" parameterType="Long">
        SELECT user_id, user_name, user_email
        FROM users
        WHERE user_id = #{id}
    </select>
    ```

    上述示例中，`parameterType` 指定了方法参数的类型，而 `resultMap` 则指定了查询结果的映射规则。

    **5. 动态 SQL 操作：**

    使用动态 SQL 标签可以根据不同的条件生成不同的 SQL 片段，以实现更复杂的操作。如前面所示，您可以在 `<if>`、`<choose>`、`<when>`、`<foreach>` 等标签内编写条件判断和循环，以根据不同的情况生成 SQL 语句。

    通过组合这些基本的数据库操作，您可以构建出适用于不同业务需求的 SQL 查询和修改语句。这些基本操作是 MyBatis 提供的核心功能，让您能够有效地进行数据库交互。

- 理解如何使用注解方式进行 CRUD 操作。

  - MyBatis 也支持使用注解方式进行 CRUD（增、删、改、查）操作，可以使用注解来代替 XML 映射文件。以下是使用注解方式进行 CRUD 操作的示例：

    **1. 插入数据（增加）：**

    ```java
    @Insert("INSERT INTO users (user_name, user_email) VALUES (#{username}, #{email})")
    int insertUser(User user);
    ```

    **2. 更新数据：**

    ```java
    @Update("UPDATE users SET user_name = #{username}, user_email = #{email} WHERE user_id = #{id}")
    int updateUser(User user);
    ```

    **3. 删除数据：**

    ```java
    @Delete("DELETE FROM users WHERE user_id = #{id}")
    int deleteUserById(Long id);
    ```

    **4. 查询数据：**

    ```java
    @Select("SELECT user_id, user_name, user_email FROM users WHERE user_id = #{id}")
    @Results(id = "UserResultMap", value = {
        @Result(property = "id", column = "user_id"),
        @Result(property = "username", column = "user_name"),
        @Result(property = "email", column = "user_email")
    })
    User getUserById(Long id);
    ```

    在上述示例中，通过在方法上使用 `@Insert`、`@Update`、`@Delete` 和 `@Select` 注解，您可以将 SQL 语句直接嵌入到 Java 方法中，从而实现对数据库的增、删、改、查操作。

    注意，为了使查询结果能够正确映射到 Java 对象，还需要使用 `@Results` 和 `@Result` 注解定义结果映射规则。

    使用注解方式可以简化代码，使得操作更加直观和紧凑。但需要注意的是，注解方式可能会导致 SQL 语句和 Java 代码耦合度较高，不太适合于较为复杂的 SQL 映射和业务逻辑。根据实际需求，您可以选择使用注解方式或 XML 映射文件方式进行数据库操作。