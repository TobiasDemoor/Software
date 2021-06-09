"Sublcasses should be substitutable for their base classes." (Contratos)
> "What is wanted here is something like the following substitution property: If for each object o1 of type S there is an object o2 of type T such that for all programs P defined in terms of T, the behavior of P is unchanged when o1 is substituted for o2 then S is a subtype of T." (- Liskov)

Informally, software (methods, classes, ...) that refers to a type T (some interface or abstract superclass) should work properly or as expected with any substituted implementation or subclass of T—call it S.