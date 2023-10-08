> 作为一名开发者踩过的坑

1. 遵循java语言规范，重写hashCode和equals方法

   不重写hashCode和equals方法的自定义类不应该在Set中使用

2. `Spring 的 BeanUtils.copyProperties`

   不能拷贝不同类型的属性

3. 初始化泛型对象时，推荐使用`diamond`语法

   > Map<String, Object> map = new HashMap<>(16);
   >
   > 编译器中可以有效提示类型不一致问题

4. 三元表达式拆装包

   > boolean condition = false;
   >
   > Double value1 = 1.0D;
   >
   > Double value2 = 2.0D;
   >
   > Double value3 = null;
   >
   > Double result = condition ? value1 * value2 : value3;// 抛出空指针异常

   三元表达式中的类型转化规则

   - 若两个表达式类型相同，返回值类型为该类型；

   - 若两个表达式类型不同，但类型不可转换，返回值类型为 Object 类型；

   - 若两个表达式类型不同，但类型可以转化，先把包装数据类型转化为基本数据类型，然后按照基本数据类型的转换规则（byte<short(char)<int<long<float<double）来转化，返回值类型为优先级最
     高的基本数据类型。

   - `尽量避免使用三元表达式，可采用if-else来代替`

   - `尽量使用基本数据类型，避免包装数据类型的拆装包`

     