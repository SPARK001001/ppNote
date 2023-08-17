SQL 语句：

### 理解如何在映射文件中编写 SQL 查询语句。

- 在 MyBatis 的映射文件中，您可以使用 `<select>`、`<insert>`、`<update>` 和 `<delete>` 元素来编写 SQL 查询、插入、更新和删除语句。以下是如何在映射文件中编写 SQL 查询语句的示例：

  **1. 编写查询语句：**

  假设我们有一个 `User` 表，您可以通过以下方式编写查询语句：

  ```xml
  <select id="getUserById" resultMap="UserResultMap">
      SELECT user_id, user_name, user_email
      FROM users
      WHERE user_id = #{id}
  </select>
  ```

  在上述示例中，`id` 是映射方法的参数，`#{id}` 是占位符，表示将方法参数的值插入到 SQL 语句中。

  **2. 使用动态 SQL：**

  MyBatis 支持动态 SQL，可以根据条件构建不同的 SQL 语句。例如，使用 `<if>`、`<choose>`、`<when>` 等标签来动态生成查询条件。

  ```xml
  <select id="getUserByNameOrEmail" resultMap="UserResultMap">
      SELECT user_id, user_name, user_email
      FROM users
      <where>
          <if test="username != null">AND user_name = #{username}</if>
          <if test="email != null">OR user_email = #{email}</if>
      </where>
  </select>
  ```

  在上述示例中，使用 `<if>` 标签根据条件动态生成不同的查询条件。

  **3. 使用参数映射：**

  您可以通过 `<parameterMap>` 或 `<parameterType>` 元素来定义方法参数的映射关系，然后在 SQL 中直接使用映射的参数名称。

  ```xml
  <parameterMap type="java.util.Map" id="userParamMap">
      <parameter property="id" jdbcType="BIGINT"/>
      <!-- 其他参数映射... -->
  </parameterMap>
  
  <select id="getUserById" resultMap="UserResultMap" parameterMap="userParamMap">
      SELECT user_id, user_name, user_email
      FROM users
      WHERE user_id = #{id}
  </select>
  ```

  **4. 使用动态 SQL片段：**

  您可以通过 `<sql>` 元素定义动态 SQL 片段，然后在其他 SQL 语句中引用这些片段。

  ```xml
  <sql id="userColumns">
      user_id, user_name, user_email
  </sql>
  
  <select id="getUserById" resultMap="UserResultMap">
      SELECT <include refid="userColumns"/>
      FROM users
      WHERE user_id = #{id}
  </select>
  ```

  通过上述示例，您可以在 MyBatis 的映射文件中编写各种类型的 SQL 查询语句，使用动态 SQL 和参数映射来满足不同的查询需求。

### 了解 MyBatis 的动态 SQL 特性，如 `<if>`、`<choose>`、`<foreach>` 等标签的使用。

- MyBatis 的动态 SQL 特性允许您根据不同的条件生成不同的 SQL 语句，以适应不同的查询需求。以下是一些常用的动态 SQL 标签的使用示例：

  **1. `<if>` 标签：**

  `<if>` 标签用于根据条件动态生成 SQL 片段。

  ```xml
  <select id="getUserByCondition" resultMap="UserResultMap">
      SELECT user_id, user_name, user_email
      FROM users
      WHERE 1=1
      <if test="username != null">AND user_name = #{username}</if>
      <if test="email != null">AND user_email = #{email}</if>
  </select>
  ```

  **2. `<choose>` 和 `<when>` 标签：**

  `<choose>` 标签类似于 Java 中的 switch 语句，`<when>` 标签用于指定每个条件分支。

  ```xml
  <select id="getUserByAgeRange" resultMap="UserResultMap">
      SELECT user_id, user_name, user_email
      FROM users
      WHERE 1=1
      <choose>
          <when test="age &lt; 18">AND user_age &lt; 18</when>
          <when test="age &gt;= 18">AND user_age &gt;= 18</when>
      </choose>
  </select>
  ```

  **3. `<foreach>` 标签：**

  `<foreach>` 标签用于遍历集合，并将集合中的元素插入到 SQL 中。

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

  在上述示例中，`userIDs` 是一个集合，`<foreach>` 标签会将集合中的元素逐个插入到 SQL 中。

  这些动态 SQL 标签可以根据不同的条件生成不同的 SQL 片段，帮助您更灵活地构建查询语句。您可以根据需要组合这些标签，以满足复杂的查询逻辑和业务需求。