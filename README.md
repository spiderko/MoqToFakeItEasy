# MoqToFakeItEasy

using Moq; => using FakeItEasy;

private Mock<IClassName> _mockClassName = null!; => private IClassName _mockClassName = null!;
_mockClassName = new Mock<ClassName>(); => _mockClassName = A.Fake<ClassName>();
_mockClassName.Setup(x => x.MethodName()).Returns(response); => A.CallTo(() => _mockClassName.MethodName()).Returns(response);
_mockClassName.Verify(x => x.MethodName(), Times.Once); => A.CallTo(() => _mockClassName.MethodName()).MustHaveHappenedOnceExactly();
