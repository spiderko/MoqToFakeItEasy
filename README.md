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

## Injecting Mock into tested class
**Moq:**
```C#
_systemUnderTest = new SystemUnderTest(_mockClassName.Object);
```

**FakeItEasy:**
```C#
_systemUnderTest = new SystemUnderTest(_mockClassName);
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

**Moq:**
```C#
_mockClassName.Verify(mock => mock.MethodName(It.Is<int>(body =>
    body.PropertyValueOne == valueOne &&
    body.PropertyValueTwo == valueTwo
)));
```

**FakeItEasy:**
```C#
A.CallTo(() => _mockClassName.MethodName(A<int>.That.Matches(body =>
        body.PropertyValueOne == valueOne &&
        body.PropertyValueTwo == valueTwo
    )));
```
Moq default behaviour when we do not specify return for a method is to return null.
FakeItEasy, on other hand, is returning empty object instead - that is why sometime I have to add specific stup for a method which runs inside of my tested class.

**Moq:**
```C#
// Nothing specified here for return from _mockClassName.GetById(1)
```

**FakeItEasy:**
```C#
A.CallTo(() => _mockClassName.GetById(1)).Returns(Task.FromResult<ReturnType>(null));
```

