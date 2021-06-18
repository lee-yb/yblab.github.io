# Object Class

Object 클래스는 자바에서 모든 클래스의 조상이다. 이 클래스에는 모든 클래스가 공통으로 포함하고 있어야 하는 기능을 제공하고 있다.

Object 클래스에 정의되어 있는 메소드를 살펴보자.



## getClass()

```java

    /**
     * Returns the runtime class of this {@code Object}. The returned
     * {@code Class} object is the object that is locked by {@code
     * static synchronized} methods of the represented class.
     *
     * <p><b>The actual result type is {@code Class<? extends |X|>}
     * where {@code |X|} is the erasure of the static type of the
     * expression on which {@code getClass} is called.</b> For
     * example, no cast is required in this code fragment:</p>
     *
     * <p>
     * {@code Number n = 0;                             }<br>
     * {@code Class<? extends Number> c = n.getClass(); }
     * </p>
     *
     * @return The {@code Class} object that represents the runtime
     *         class of this object.
     * @jls 15.8.2 Class Literals
     */
    @HotSpotIntrinsicCandidate
    public final native Class<?> getClass();
```

자신이 속한 클래스의 **[Class객체](./2020-06-17-Class-class)**를 반환하는 메서드인데, 쉽게말해 **현재 참조하고 있는 클래스를 확인할 수 있는 메소드**이다. ```System.out.println(a.getClass());``` 의 결과로 ```class java.lang.Object``` 이라면 a 는 java.lang 패키지의 Object 클래스의 인스턴스이다.



## equals(Object obj)

```java
/**
     * Indicates whether some other object is "equal to" this one.
     * <p>
     * The {@code equals} method implements an equivalence relation
     * on non-null object references:
     * <ul>
     * <li>It is <i>reflexive</i>: for any non-null reference value
     *     {@code x}, {@code x.equals(x)} should return
     *     {@code true}.
     * <li>It is <i>symmetric</i>: for any non-null reference values
     *     {@code x} and {@code y}, {@code x.equals(y)}
     *     should return {@code true} if and only if
     *     {@code y.equals(x)} returns {@code true}.
     * <li>It is <i>transitive</i>: for any non-null reference values
     *     {@code x}, {@code y}, and {@code z}, if
     *     {@code x.equals(y)} returns {@code true} and
     *     {@code y.equals(z)} returns {@code true}, then
     *     {@code x.equals(z)} should return {@code true}.
     * <li>It is <i>consistent</i>: for any non-null reference values
     *     {@code x} and {@code y}, multiple invocations of
     *     {@code x.equals(y)} consistently return {@code true}
     *     or consistently return {@code false}, provided no
     *     information used in {@code equals} comparisons on the
     *     objects is modified.
     * <li>For any non-null reference value {@code x},
     *     {@code x.equals(null)} should return {@code false}.
     * </ul>
     * <p>
     * The {@code equals} method for class {@code Object} implements
     * the most discriminating possible equivalence relation on objects;
     * that is, for any non-null reference values {@code x} and
     * {@code y}, this method returns {@code true} if and only
     * if {@code x} and {@code y} refer to the same object
     * ({@code x == y} has the value {@code true}).
     * <p>
     * Note that it is generally necessary to override the {@code hashCode}
     * method whenever this method is overridden, so as to maintain the
     * general contract for the {@code hashCode} method, which states
     * that equal objects must have equal hash codes.
     *
     * @param   obj   the reference object with which to compare.
     * @return  {@code true} if this object is the same as the obj
     *          argument; {@code false} otherwise.
     * @see     #hashCode()
     * @see     java.util.HashMap
     */
    public boolean equals(Object obj) {
        return (this == obj);
    }
```

**매개변수로 객체의 참조변수를 받아서 비교하여 결과를 boolean값으로 알려 주는 메서드**이다.

코드에서 알수 있듯이 두 객체의 같고 다름을 **```참조변수의 값```**으로 판단한다. 그렇기 때문에 서로 다른 객체를 비교하면 항상 false이다.

알고 있듯이 비교연산자 "==" 는 주소값을 비교하고 equals() 메소드는 데이터 값을 비교한다고 알고 있는데, 이는 비교하는 값클래스들이 값을 비교할수 있도록 equals 메서드를 **```오버라이딩```**하였기 때문이다

> #### ex. String 클래스의 equals()
>
> ```java
> public boolean equals(Object anObject) {
>         if (this == anObject) {
>             return true;
>         }
>         if (anObject instanceof String) {
>             String aString = (String)anObject;
>             if (coder() == aString.coder()) {
>                 return isLatin1() ? StringLatin1.equals(value, aString.value)
>                                   : StringUTF16.equals(value, aString.value);
>             }
>         }
>         return false;
>     }
> ```
>
> #### ex. Integer 클래스의 equals()
>
> ```java
> public boolean equals(Object obj) {
>         if (obj instanceof Integer) {
>             return value == ((Integer)obj).intValue();
>         }
>         return false;
>     }
> ```

이렇게 함으로써 서로 다른 인스턴스일지라도 같은 값을 가지고 있다면 equals로 비교했을때 true를 결과로 얻을 수 있다.



## hashCode()

해싱기법에 사용되는 ```해시함수``` 를 구현한 것이다. 일반적으로 **객체의 주소값을 변환하여 생성한 객체의 고유한 정수값**이다.

hashCode는 HashTable과 같은 자료구조를 사용할 때 데이터가 저장되는 위치를 결정하기 위해 사용된다.

Object 클래스에 정의된 hashCode 메서드는 객체의 주소값을 이용해서 해시코드를 만들어 반환하기 때문에 서로 다른 두 객체는 결코 같은 해시코드를 가질 수 없다.

```java
/**
     * Returns a hash code value for the object. This method is
     * supported for the benefit of hash tables such as those provided by
     * {@link java.util.HashMap}.
     * <p>
     * The general contract of {@code hashCode} is:
     * <ul>
     * <li>Whenever it is invoked on the same object more than once during
     *     an execution of a Java application, the {@code hashCode} method
     *     must consistently return the same integer, provided no information
     *     used in {@code equals} comparisons on the object is modified.
     *     This integer need not remain consistent from one execution of an
     *     application to another execution of the same application.
     * <li>If two objects are equal according to the {@code equals(Object)}
     *     method, then calling the {@code hashCode} method on each of
     *     the two objects must produce the same integer result.
     * <li>It is <em>not</em> required that if two objects are unequal
     *     according to the {@link java.lang.Object#equals(java.lang.Object)}
     *     method, then calling the {@code hashCode} method on each of the
     *     two objects must produce distinct integer results.  However, the
     *     programmer should be aware that producing distinct integer results
     *     for unequal objects may improve the performance of hash tables.
     * </ul>
     * <p>
     * As much as is reasonably practical, the hashCode method defined
     * by class {@code Object} does return distinct integers for
     * distinct objects. (The hashCode may or may not be implemented
     * as some function of an object's memory address at some point
     * in time.)
     *
     * @return  a hash code value for this object.
     * @see     java.lang.Object#equals(java.lang.Object)
     * @see     java.lang.System#identityHashCode
     */
    @HotSpotIntrinsicCandidate
    public native int hashCode();
```

클래스의 인스턴스변수 값으로 객체의 같고 다름을 판단해야하는 경우라면 equals메서드 뿐 아니라 hashCode메서드도 적절히 오버라이딩해야 한다.

> #### ex. Object 클래스의 hashCode()
>
> 참고) [How does the default hashCode() work?](https://srvaroa.github.io/jvm/java/openjdk/biased-locking/2017/01/30/hashCode.html)
>
> #### ex. String 클래스의 hashCode()
>
> ```java
> public int hashCode() {
>         int h = hash;
>         if (h == 0 && value.length > 0) {
>             hash = h = isLatin1() ? StringLatin1.hashCode(value)
>                                   : StringUTF16.hashCode(value);
>         }
>         return h;
>     }
> 
> private boolean isLatin1() {
>         return COMPACT_STRINGS && coder == LATIN1;
>     }
> 
> private final byte coder;
> static final boolean COMPACT_STRINGS;
> 
>     static {
>         COMPACT_STRINGS = true;
>     }
> @Native static final byte LATIN1 = 0;
> @Native static final byte UTF16  = 1;
> 
> final class StringLatin1 {
>   	public static int hashCode(byte[] value) {
>         int h = 0;
>         for (byte v : value) {
>             h = 31 * h + (v & 0xff);
>         }
>         return h;
>     }
> }
> 
> final class StringUTF16 {
>   	public static int hashCode(byte[] value) {
>         int h = 0;
>         int length = value.length >> 1;
>         for (int i = 0; i < length; i++) {
>             h = 31 * h + getChar(value, i);
>         }
>         return h;
>     }
> }
> ```
>
> #### ex. Integer 클래스의 hashCode()
>
> ```java
> @Override
>     public int hashCode() {
>         return Integer.hashCode(value);
>     }
> 
>     public static int hashCode(int value) {
>         return value;
>     }
> ```
>
> 

```java
public class Main {

    public static void main(String[] args) {
        Object obj = new Object();
        Object obj2 = new Object();
        String str = new String("123");
        String str2 = new String("123");
        Integer i = new Integer(123);
        Integer i2 = new Integer(123);

        System.out.println(obj.hashCode());                 //1057941451
        System.out.println(System.identityHashCode(obj));   //1057941451
        System.out.println(obj2.hashCode());                //1975358023
        System.out.println();

        System.out.println(str.hashCode());                 //48690
        System.out.println(System.identityHashCode(str));   //2101440631
        System.out.println(str2.hashCode());                //48690
        System.out.println();

        System.out.println(i.hashCode());                   //123
        System.out.println(System.identityHashCode(i));     //2109957412
        System.out.println(i2.hashCode());                  //123
    }
}
```

String 클래스는 문자열의 내용이 같으면, 동일한 해시코드를 반환하도록 오버라이딩 되어 있기 때문에, 문자열 내용이 같은 인스턴스에 대해 hashCode()를 호출하면 항상 동일한 해시코드값을 얻는다.



### equals와 hashCode의 관계

_동일한 객체는 동일한 메모리 주소를 갖는다는 것을 의미하므로, 동일한 객체는 동일한 해시코드를 가져야 한다._ 그렇기 때문에 _**equals() 메소드를 오버라이드 한다면, hashCode() 메소드도 오버라이드 되어야 한다.**_

참고) https://mangkyu.tistory.com/101



## toString()

**인스턴스에 대한 정보를 문자열(String)로 제공할 목적**으로 정의한 것.

```java
/**
     * Returns a string representation of the object. In general, the
     * {@code toString} method returns a string that
     * "textually represents" this object. The result should
     * be a concise but informative representation that is easy for a
     * person to read.
     * It is recommended that all subclasses override this method.
     * <p>
     * The {@code toString} method for class {@code Object}
     * returns a string consisting of the name of the class of which the
     * object is an instance, the at-sign character `{@code @}', and
     * the unsigned hexadecimal representation of the hash code of the
     * object. In other words, this method returns a string equal to the
     * value of:
     * <blockquote>
     * <pre>
     * getClass().getName() + '@' + Integer.toHexString(hashCode())
     * </pre></blockquote>
     *
     * @return  a string representation of the object.
     */
    public String toString() {
        return getClass().getName() + "@" + Integer.toHexString(hashCode());
    }	
```

toString()은 일반적으로 인스턴스나 클래스에 대한 정보 또는 인스턴스 변수들의 값을 문자열로 변환하여 반환하도록 오버라이딩 되는 것이 보통이다.



## clone()

**자신을 복제하여 새로운 인스턴스를 생성**하는 일을 한다. 원래의 인스턴스는 보존하여 작업에 실패해서 원래의 상태로 되돌리거나 변경되기 전의 값을 참고하는 도움이 되게 하기 위하여 만든 메서드이다.

```java
		/**
     * Creates and returns a copy of this object.  The precise meaning
     * of "copy" may depend on the class of the object. The general
     * intent is that, for any object {@code x}, the expression:
     * <blockquote>
     * <pre>
     * x.clone() != x</pre></blockquote>
     * will be true, and that the expression:
     * <blockquote>
     * <pre>
     * x.clone().getClass() == x.getClass()</pre></blockquote>
     * will be {@code true}, but these are not absolute requirements.
     * While it is typically the case that:
     * <blockquote>
     * <pre>
     * x.clone().equals(x)</pre></blockquote>
     * will be {@code true}, this is not an absolute requirement.
     * <p>
     * By convention, the returned object should be obtained by calling
     * {@code super.clone}.  If a class and all of its superclasses (except
     * {@code Object}) obey this convention, it will be the case that
     * {@code x.clone().getClass() == x.getClass()}.
     * <p>
     * By convention, the object returned by this method should be independent
     * of this object (which is being cloned).  To achieve this independence,
     * it may be necessary to modify one or more fields of the object returned
     * by {@code super.clone} before returning it.  Typically, this means
     * copying any mutable objects that comprise the internal "deep structure"
     * of the object being cloned and replacing the references to these
     * objects with references to the copies.  If a class contains only
     * primitive fields or references to immutable objects, then it is usually
     * the case that no fields in the object returned by {@code super.clone}
     * need to be modified.
     * <p>
     * The method {@code clone} for class {@code Object} performs a
     * specific cloning operation. First, if the class of this object does
     * not implement the interface {@code Cloneable}, then a
     * {@code CloneNotSupportedException} is thrown. Note that all arrays
     * are considered to implement the interface {@code Cloneable} and that
     * the return type of the {@code clone} method of an array type {@code T[]}
     * is {@code T[]} where T is any reference or primitive type.
     * Otherwise, this method creates a new instance of the class of this
     * object and initializes all its fields with exactly the contents of
     * the corresponding fields of this object, as if by assignment; the
     * contents of the fields are not themselves cloned. Thus, this method
     * performs a "shallow copy" of this object, not a "deep copy" operation.
     * <p>
     * The class {@code Object} does not itself implement the interface
     * {@code Cloneable}, so calling the {@code clone} method on an object
     * whose class is {@code Object} will result in throwing an
     * exception at run time.
     *
     * @return     a clone of this instance.
     * @throws  CloneNotSupportedException  if the object's class does not
     *               support the {@code Cloneable} interface. Subclasses
     *               that override the {@code clone} method can also
     *               throw this exception to indicate that an instance cannot
     *               be cloned.
     * @see java.lang.Cloneable
     */
    @HotSpotIntrinsicCandidate
    protected native Object clone() throws CloneNotSupportedException;
```

Object 클래스에 정의된 clone()은 _인스턴스변수의 값만을 복사하기 때문에 참조타입의 인스턴스 변수가 있는 클래스는 완전한 인스턴스 복제가 이루어지지 않는다._

예를들어 배열의 경우 복제된 인스턴스도 같은 배열의 주소를 갖기 때문에 복제된 인스턴스의 작업이 원래의 인스턴스에 영향을 미치게 된다. 그렇기 때문에 오버라이딩해서 clone 메서드를 구현하여야 한다.

clone() 을 사용하기 위해서는 복제할 클래스가 ```Cloneable 인터페이스```를 구현해야하고, 오버라이드 된 clone() 의 ```접근 제어자를 public``` 으로 변경한다. 그래야 상속관계가 없는 다른 클래스에서 clone()을 호출할 수 있다.

```java
package java.lang;

/**
 * A class implements the <code>Cloneable</code> interface to
 * indicate to the {@link java.lang.Object#clone()} method that it
 * is legal for that method to make a
 * field-for-field copy of instances of that class.
 * <p>
 * Invoking Object's clone method on an instance that does not implement the
 * <code>Cloneable</code> interface results in the exception
 * <code>CloneNotSupportedException</code> being thrown.
 * <p>
 * By convention, classes that implement this interface should override
 * {@code Object.clone} (which is protected) with a public method.
 * See {@link java.lang.Object#clone()} for details on overriding this
 * method.
 * <p>
 * Note that this interface does <i>not</i> contain the {@code clone} method.
 * Therefore, it is not possible to clone an object merely by virtue of the
 * fact that it implements this interface.  Even if the clone method is invoked
 * reflectively, there is no guarantee that it will succeed.
 *
 * @author  unascribed
 * @see     java.lang.CloneNotSupportedException
 * @see     java.lang.Object#clone()
 * @since   1.0
 */
public interface Cloneable {
}
```

Cloneable 인터페이스를 구현하게 하는 이유는 인스턴스의 데이터를 보호하기 위해서이다. _**Cloneable 인터페이스가 구현되어 있다는 것은 클래스 작성자가 복제를 허용한다는 의미**_이다.



### 얕은복사 와 깊은복사

clone()은 단순히 객체에 저장된 값을 그대로 복제할 뿐, 객체가 참조하고 있는 객체까지 복제하지는 않는다.

배열인 경우를 예로들면 기본형 배열인 경우에는 아무런 문제가 없지만, 객체배열을 clone()으로 복제하는 경우에는 **원본과 복제본이 같은 객체를 공유**하므로 완전한 복제라고 보기 어렵다. 이러한 복제를 ```얕은복사(shallow copy)```라고 한다.

반면에 **원본이 참조하고 있는 객체까지 복제**하는 것을 ```깊은복사(deep copy)```라고 하며, 원본의 변경이 복사본에 영향을 미치지 않는다.