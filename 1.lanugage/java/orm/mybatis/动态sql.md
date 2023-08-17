动态 SQL：**

- 知道如何使用 MyBatis 的动态 SQL 特性来构建动态的查询语句。

  - MyBatis 的动态 SQL 特性允许您根据不同的条件动态构建查询语句，从而灵活地满足不同的查询需求。以下是一些动态 SQL 的示例用法：

    **1. 使用 `<if>` 标签：**
    可以根据条件生成不同的 SQL 片段。

    ```xml
    <select id="getUserByCondition" resultMap="UserResultMap">
        SELECT user_id, user_name, user_email
        FROM users
        WHERE 1=1
        <if test="username != null">AND user_name = #{username}</if>
        <if test="email != null">AND user_email = #{email}</if>
    </select>
    ```

    **2. 使用 `<choose>` 和 `<when>` 标签：**
    实现类似于 switch-case 的条件判断。

    ```xml
    <select id="getUserByAgeRange" resultMap="UserResultMap">
        SELECT user_id, user_name, user_email
        FROM users
        WHERE 1=1
        <choose>
            <when test="age &lt; 18">AND user_age &lt; 18</when>
            <when test="age &gt;= 18">AND user_age &gt;= 18</when>
            <otherwise>AND user_age IS NULL</otherwise>
        </choose>
    </select>
    ```

    **3. 使用 `<foreach>` 标签：**
    遍历集合，生成多次重复的 SQL 片段。

    ```xml
    <select id="getUsersByIDs" resultMap="UserResultMap">
        SELECT user_id, user_name, user_email
        FROM users
        WHERE user_id IN
        <foreach item="id" collection="userIDs" open="(" separator="," close=")">
            #{id}
        </foreach>
    </select>
    ```

    **4. 使用 `<trim>` 标签：**
    可以去除或添加 SQL 语句中的不必要部分。

    ```xml
    <select id="getUserByCondition" resultMap="UserResultMap">
        SELECT user_id, user_name, user_email
        FROM users
        <trim prefix="WHERE" prefixOverrides="AND | OR">
            <if test="username != null">AND user_name = #{username}</if>
            <if test="email != null">AND user_email = #{email}</if>
        </trim>
    </select>
    ```

    上述示例展示了动态 SQL 的一些常见用法。您可以根据业务需求，结合这些标签和条件，构建灵活的查询语句。使用动态 SQL 特性，可以避免在不同情况下编写大量重复的查询语句，提高代码的可维护性和灵活性。