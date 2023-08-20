# Migration from Moq to FakeItEasy

## Using
**Moq:**
```
using Moq; 
```

**FakeItEasy:**
```
using FakeItEasy;
```

## Declaration of the new vairiable which will hold Mock
**Moq:**
```
private Mock<IClassName> _mockClassName = null!; 
```

**FakeItEasy:**
```
private IClassName _mockClassName = null!;
```

## Initiation of the new Mock
**Moq:**
```
_mockClassName = new Mock<ClassName>();
```

**FakeItEasy:**
```
_mockClassName = A.Fake<ClassName>();
```

## Setting up behaviour of the method
**Moq:**
```
_mockClassName.Setup(x => x.MethodName()).Returns(response);
```

**FakeItEasy:**
```
A.CallTo(() => _mockClassName.MethodName()).Returns(response);
```

**Moq:**
```
_mockClassName.Setup(x => x.MethodName(It.IsAny<int>(), It.IsAny<string>())).Returns(response);
```

**FakeItEasy:**
```
A.CallTo(() => _mockClassName.MethodName(A<int>._, A<string>._)).Returns(response);
```

```A<int>._``` is a shorthand declaration of ```A<int>.Ignored```. It is equivalent of ```It.IsAny<int>()``` in Moq.

## Veryfing if method run once
**Moq:**
```
_mockClassName.Verify(x => x.MethodName(), Times.Once);
```

**FakeItEasy:**
```
A.CallTo(() => _mockClassName.MethodName()).MustHaveHappenedOnceExactly();
```

**Moq:**
```
_mockClassName.Verify(x => x.MethodName(A<int>._, A<string>._), Times.Once);
```

**FakeItEasy:**
```
A.CallTo(() => _mockClassName.MethodName(A<int>._, A<string>._)).MustHaveHappenedOnceExactly();
```
