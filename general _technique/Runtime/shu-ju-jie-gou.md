# 数据结构

对象与类的数据结构

## NSObject

```objc
    @interface NSObject <NSObject> {
        Class isa  OBJC_ISA_AVAILABILITY;
    }
```

`isa` 指针指向对象的`类对象`，所有实例方法存放在`类对象`的方法表内

## id

```objc

    // A pointer to an instance of a class.
    typedef struct objc_object *id;
    
    // Represents an instance of a class.
    struct objc_object {
        Class _Nonnull isa;
    };
```

## Class类对象

```objc
    
    // 代表OC类的不透明指针
    typedef struct objc_class *Class;

    struct objc_class {
        Class _Nonnull isa;

        Class _Nullable super_class; // 指向父类
        const char * _Nonnull name; // 类名
        long version;
        long info;
        long instance_size; // 实例大小
        struct objc_ivar_list * _Nullable ivars; // 实例变量列表
        struct objc_method_list * _Nullable * _Nullable methodLists; // 方法表
        struct objc_cache * _Nonnull cache; // 方法缓存
        struct objc_protocol_list * _Nullable protocols; // 属性列表

    };
    /* Use `Class` instead of `struct objc_class *` */
    
    struct objc_cache {
        unsigned int mask /* total = mask + 1 */;
        unsigned int occupied;
        Method buckets[1];
    };
```

类对象也有一个`isa`指针，指向元类，元类存储着类方法。

- `objc_method_list` 对象方法列表，类对象存储所有实例方法，元类存储所有类方法
- `objc_cache` 方法缓存，缓存对象使用过的方法

## 实例变量 Ivar

```objc

    typedef struct objc_ivar *Ivar;
    
    struct objc_ivar {
        char *ivar_name  OBJC2_UNAVAILABLE;   // 变量名
        char *ivar_type  OBJC2_UNAVAILABLE;	// 变量类型
        int ivar_offset  OBJC2_UNAVAILABLE;	// 基地址偏移字节		            
           
        #ifdef __LP64__
        int space OBJC2_UNAVAILABLE;
        #endif
    }

```

## 属性 objc_property

```objc
    
    struct property_t {
        const char *name;
        const char *attributes;
    };

    // 属性的特性
    typedef struct {
        const char *name;           // 特性名
        const char *value;          // 特性值
    } objc_property_attribute_t;
```

## 选择器 SEL 与 函数实现 IMP

```objc
    
    // 方法的selector用于表示运行时方法的名字。Objective-C在编译时，会依据每一个方法的名字、参数序列，生成一个唯一的整型标识(Int类型的地址)，这个标识就是SEL
    typedef struct objc_selector *SEL;
    
    // IMP实际上是一个函数指针，指向方法实现的首地址，SEL就是为了查找方法的最终实现IMP的
    id (*IMP)(id, SEL, ...)

```

## 方法 Method

```objc
    
    typedef struct objc_method *Method;
    struct objc_method {
        SEL method_name     OBJC2_UNAVAILABLE;	// 方法名
        char *method_types  OBJC2_UNAVAILABLE;
        IMP method_imp      OBJC2_UNAVAILABLE;	// 方法实现
    }
    
    // objc_method_description
    struct objc_method_description { SEL name; char *types; };

    
```

## 分类 Category

```objc

    typedef struct objc_category *Category;
    struct objc_category {
        char *category_name; // 分类名
        char *class_name; // 分类所属的类名
        struct objc_method_list *instance_methods;// 实例方法列表
        struct objc_method_list *class_methods;// 类方法列表
        struct objc_protocol_list *protocols;// 分类所实现的协议列表
}    
```

## 协议

```objc 
	
    typedef struct objc_object Protocol;

```

# 对象、类、元类之间的关系

- `对象`的`isa`指向`类对象`，`类对象`的`isa`指针指向`元类`，`元类`的`isa`指针都指向基类，即任何`NSObject`继承体系下的`元类`都使用`NSObject`的`元类`，作为自己所属的类，而基类的`isa`指针指向自己。

- 类的`super_class`指针指向父类，根类的`super_class`指针为nil

- 对象调用方去类对象的方法缓存中去找，如果没有就去方法表中查找，如果没有就去父类中查找，直到找到。找到后调用方法，并缓存在方法缓存中。如果没有找到就会走消息转发机制。

![](/assets/WechatIMG64077.jpeg)
