MyBatis 提供了参数绑定和预编译查询的特性，这些特性有助于防止 SQL 注入攻击。以下是使用 MyBatis 防止 SQL 注入的方法：

**1. 使用参数绑定：**
在映射文件中，始终使用 `#{parameter}` 语法来表示参数，而不是通过字符串拼接构建 SQL 查询。

```xml
<!-- 错误的示范，容易受到注入攻击 -->
<select id="getUser" parameterType="String" resultType="User">
    SELECT * FROM users WHERE username = '${username}'
</select>

<!-- 正确的示范，使用参数绑定 -->
<select id="getUser" parameterType="String" resultType="User">
    SELECT * FROM users WHERE username = #{username}
</select>
```

**2. 避免动态拼接：**
尽量避免在 SQL 查询中使用动态拼接，特别是将用户输入直接拼接到查询中。如果需要动态构建查询条件，使用 `<if>`、`<where>` 等动态 SQL 标签。

**3. 使用条件判断标签：**
在映射文件中，使用 `<if>` 标签来根据不同的条件生成 SQL 片段。

```xml
<select id="getUserByCondition" resultMap="UserResultMap">
    SELECT user_id, user_name, user_email
    FROM users
    WHERE 1=1
    <if test="username != null">AND user_name = #{username}</if>
    <if test="email != null">AND user_email = #{email}</if>
</select>
```

通过以上方法，MyBatis 会自动对参数进行转义和预编译，从而防止 SQL 注入攻击。尽管 MyBatis 的参数绑定机制可以大大降低 SQL 注入的风险，但仍建议开发人员遵循最佳实践，不要将用户输入数据直接用于 SQL 查询，以确保应用程序的安全性。