# Migration from Moq to FakeItEasy

## Using
**Moq:**
```C#
using Moq; 
```

**FakeItEasy:**
```C#
using FakeItEasy;
```

## Declaration of the new vairiable which will hold Mock
**Moq:**
```C#
private Mock<IClassName> _mockClassName = null!; 
```

**FakeItEasy:**
```C#
private IClassName _mockClassName = null!;
```

## Initiation of the new Mock
**Moq:**
```C#
_mockClassName = new Mock<ClassName>();
```

**FakeItEasy:**
```C#
_mockClassName = A.Fake<ClassName>();
```

## Setting up behaviour of the method
**Moq:**
```C#
_mockClassName.Setup(x => x.MethodName()).Returns(response);
```

**FakeItEasy:**
```C#
A.CallTo(() => _mockClassName.MethodName()).Returns(response);
```

**Moq:**
```C#
_mockClassName.Setup(x => x.MethodName(It.IsAny<int>(), It.IsAny<string>())).Returns(response);
```

**FakeItEasy:**
```C#
A.CallTo(() => _mockClassName.MethodName(A<int>._, A<string>._)).Returns(response);
```

```A<int>._``` is a shorthand declaration of ```A<int>.Ignored```. It is equivalent of ```It.IsAny<int>()``` in Moq.

## Veryfing if method run once
**Moq:**
```C#
_mockClassName.Verify(x => x.MethodName(), Times.Once);
```

**FakeItEasy:**
```C#
A.CallTo(() => _mockClassName.MethodName()).MustHaveHappenedOnceExactly();
```

**Moq:**
```C#
_mockClassName.Verify(x => x.MethodName(A<int>._, A<string>._), Times.Once);
```

**FakeItEasy:**
```C#
A.CallTo(() => _mockClassName.MethodName(A<int>._, A<string>._)).MustHaveHappenedOnceExactly();
```
