* 数据封装、继承和多态是面向对象的三大特点
* 和普通的函数相比，在类中定义的函数只有一点不同，就是第一个参数永远是实例变量self，并且，调用时，不用传递该参数。除此之外，类的方法和普通函数没有什么区别，所以，你仍然可以用默认参数、可变参数、关键字参数和命名关键字参数。
* 如果要让内部属性不被外部访问，可以把属性的名称前加上两个下划线__，在Python中，实例的变量名如果以__开头，就变成了一个私有变量（private），只有内部可以访问，外部不能访问
* 在Python中，变量名类似__xxx__的，也就是以双下划线开头，并且以双下划线结尾的，是特殊变量，特殊变量是可以直接访问的，不是private变量，所以，不能用__name__、__score__这样的变量名。
* 双下划线开头的实例变量是不是一定不能从外部访问呢？其实也不是。不能直接访问__name是因为Python解释器对外把__name变量改成了_Student__name，所以，仍然可以通过_Student__name来访问__name变量.
* 对于静态语言，如果需要传入Animal类型，则传入的对象必须是Animal类型或者它的子类，否则，将无法调用run()方法。对于Python这样的动态语言来说，则不一定需要传入Animal类型。我们只需要保证传入的对象有一个run()方法就可以了
* 使用type()函数可以判断对象类型，判断基本数据类型可以直接写int，str等，但如果要判断一个对象是否是函数怎么办？可以使用types模块中定义的常量 type(fn)==types.FunctionType
* 我们要判断class的类型，可以使用isinstance()函数，能用type()判断的基本类型也可以用isinstance()判断，isinstance([1, 2, 3], (list, tuple)) 可以判断是否是类型中的某一种
* 如果要获得一个对象的所有属性和方法，可以使用dir()函数，它返回一个包含字符串的list，比如，获得一个str对象的所有属性和方法
* 类属性
  ```py
  class Student(object):
    count = 0

    def __init__(self, name):
        self.name = name
        Student.counter()
       
    @classmethod
    def counter(cls):
        cls.count = cls.count + 1
  ```
* 使用__slots__
为了达到限制的目的，Python允许在定义class的时候，定义一个特殊的__slots__变量，来限制该class实例能添加的属性,使用__slots__要注意，__slots__定义的属性仅对当前类实例起作用，对继承的子类是不起作用的,除非在子类中也定义__slots__，这样，子类实例允许定义的属性就是自身的__slots__加上父类的__slots__
  ```
   class Student(object):
    __slots__ = ('name', 'age') # 用tuple定义允许绑定的属性名称
  ```
* 使用property定义属性
  ```
  class Screen(object):
    @property
    def width(self):
        return self._width

    @width.setter
    def width(self,value):
        self._width = value  

    @property
    def height(self):
        return self._height

    @height.setter
    def height(self,value):
        self._height = value  

    @property
    def resolution(self):
        self._resolution =   self._height * self._width
        return self._resolution
  ```  
* 多重继承,通过多重继承，一个子类就可以同时获得多个父类的所有功能
  ```
  class Dog(Mammal, Runnable):
    pass
  ```
  
* 定制类，Python的class中还有许多这样有特殊用途的函数，可以帮助我们定制类。
  ```
  当调用不存在的属性时，比如score，Python解释器会试图调用__getattr__(self, 'score')来尝试获得属性，这样，我们就有机会返回score的值：
  
  class Student(object):

    def __init__(self):
        self.name = 'Michael'

    def __getattr__(self, attr):
        if attr=='score':
            return 99
  ```
  
* 枚举类

  @unique
class Gender(Enum):
    Male = 0
    Female = 1
class Student(object):
    def __init__(self, name, gender = 0):    # 初始化输入参数gender可以是Gender类的枚举成员，同时也可以是枚举成员的名称或值
        self.name = name
        if isinstance(gender, Gender):    # gender为枚举成员
            self.gender = gender

        elif isinstance(gender, str):    # gender为枚举成员的名称
            if gender.capitalize() in Gender.__members__.keys():    # Enum的特殊属性__members__是一个将名称映射到枚举成员的字典
                self.gender = Gender[gender.capitalize()]
            else:
                raise ValueError('%s is not a valid gender' % gender)
                            
        elif isinstance(gender, int):    # gender为枚举成员的值
            if gender in Gender._value2member_map_:    # Enum的属性_value2member_map_是包含所有枚举成员的值的列表
                self.gender = Gender(gender)
            else:
                raise ValueError('%s is not a valid gender' % gender)

        else:
            raise ValueError('%s is not a valid gender' % gender)            
        
alan = Student('Alan', 0)
bart = Student('Bart', Gender.Male)
cathy = Student('Cathy', 'female')
for i in [alan, bart, cathy]:
    print(i.gender)
  