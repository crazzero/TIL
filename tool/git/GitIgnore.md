# π« GitIgnore

git μΌλ‘ μμν  λ, commitμ ν¬ν¨μν€κ³  μΆμ§ μμ λκ° μλ€.  
commit μ ν¬ν¨μν€μ§ μκΈ° μν΄μλ κ·Έ κ·μΉμ ν΄λΉ repository μ΅μμμ .gitignore λ₯Ό λ§λ€κ³   
ν΄λΉ νμΌμ κ·μΉλ€μ μ μ΄ λ£μ΄μ£Όλ©΄ λλ€.

Itellij κΈ°λ°μ μ’μ IDEμμλ gitignore νμΌμ λ΄λΆμμ λ§λ€ μλ μκ³ ,  
AndroidStudio λ±μμ νλ‘μ νΈ μμ±μμ μλμΌλ‘ gitignore νμΌμ΄ λ§λ€μ΄μ§λ κ²μ νμΈν  μ μλ€.  
νμ§λ§, μλμΌλ‘ λ§λ€μ΄μ§ νμΌλ€μ μνλ λ΄μ©μ΄ λ€μ΄κ° μμ§ μμ κ²½μ°κ° λ§μΌλ―λ‘  
μ΄ λ¬Έμμμλ μ¨λΌμΈ μΉμ¬μ΄νΈμμ gitignore νμΌμ λ§λλ λ°©λ² + μ»€μ€ν νλ λ°©λ²μ λν΄μ μ€λͺνλ €κ³  νλ€.

## μΉμ¬μ΄νΈμμ gitignore νμΌ λ§λ€κΈ°

1. [toptal-gitignore](https://www.toptal.com/developers/gitignore) μ¬μ΄νΈμ μ μνλ€.
2. μ νν gitignore νμΌ μμ±μ μν΄ μλ λ΄μ©μ μ μ΄μ€λ€.  
  - OS (MacOS, Linux, Windows, etc...)
  - IDEs (Visual Studio Code, Intellij, Android Studio, etc...)
  - Programming Languages (Java, Kotlin, Python, etc...)
  - Framework (OpenFrameworks, Firebase, etc...)
3. μ΄λ κ² μΆκ°ν΄μ£Όκ³  λ ν create λ²νΌμ λλ¬μ£Όλ©΄, μμ°½μ΄ μ΄λ¦¬λ©΄μ gitignore νμΌμ μ§μ΄λ£μ λ΄μ©μ΄ λμ¨λ€.  
4. ν΄λΉ νμ€νΈλ₯Ό gitignore νμΌμ λ£κΈ°λ§ νλ©΄ λλ€.

## gitignore μ»€μ€ννκΈ°

μν©μ λ°λΌμ gitignore νμΌμ μλ΄μΌ λλ κ²½μ°λ λλ¬(?) μλ€.
μ΄ κ²½μ°μλ μλ λ¬Έλ²μ λ§κ² μνλ λΆλΆμ μΆκ°ν΄μ£Όλ©΄ λλ€.

| Pattern Format | Description |
| --- | --- |
| `blank line(κ³΅λ°±)` | κ³΅λ°±μ μλ¬΄λ° μ­ν λ νμ§ μλλ€. λ¨μν λ΄μ© λΆλ¦¬μ κ°λμ±μ μν΄ μ‘΄μ¬νλ€. |
| `hash(#)` | μ£Όμμ μλ―Ένλ€. (e.g. # This is comment) |
| `asterisks(*)` | λͺ¨λ μ μλ―Ένλ€. |
| `Two consecutive asterisks(**)` | λ λμ μλ―Έμ λͺ¨λ μ μλ―Ένλ€. |
| `important mark(!)` | μμ ! κ° λΆμ΄μλ λΆλΆμ ignore μμ μ μΈμν¨λ€. (e.g. !src) |
| `*.foo` | λͺ¨λ  νμ₯μκ° foo μΈ νμΌλ€μ ignore μν¨λ€. |
| `/*.foo` | νμ¬ ν΄λμ λͺ¨λ  νμ₯μκ° foo μΈ νμΌλ€μ ignore μν¨λ€. |
| `foo.*` | foo λ‘ μμνλ λͺ¨λ  νμΌ λ° ν΄λλ€μ ignore μν¨λ€. |
| `**/foo` | λͺ¨λ  foo λ₯Ό ignore μν¨λ€. |
| `/**/foo` | νμ¬ ν΄λμ λͺ¨λ  foo λ₯Ό ignore μν¨λ€. |
| `a/**/b` | a ν΄λ μμμλ λͺ¨λ  b λ₯Ό ignore μν¨λ€. (e.g. `a/b`, `a/x/b`, `a/x/y/b`) |

νλ‘μ νΈ μ μ²΄μμ `foo/bar` λ§μ μΆκ°νκ³  μΆμ κ²½μ°μλ μλμ²λΌ μΆκ°ν΄μ£Όλ©΄ λλ€.  

```gitignore
/*
!/foo
/foo/*
!/foo/bar
```

