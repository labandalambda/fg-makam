

# fg.makam

This is the first file we worked on and the best starting point for the project. Here we define all the necessary types and constructors to define Featherweight Go's Abstract Syntax Tree.

Our representation of Featherweight Go is typical of how you represent a language in functional programming languages. Each node has a type associated with it, and each construct in the language has an associated constructor. For example, an expression is represented by the "expr" datatype. For each expression constructor in the calculus, we define a constructor for the "expr" datatype in Makam. Expressions in Go can be struct literals, method calls, field access or type assertions. So there will be a constructor for each of them.

Like this

```
expr: type.

method_call : expr -> string -> list expr -> expr.
struct_lit : string -> list expr -> expr.
select : expr -> string -> expr.
type_ass : expr -> string -> expr.
```

Which means, ```expr``` is a type, and both ```method_call``` and ```struct_lit``` are constructors for the type.

The representation we use is based on the FG calculus, whose syntax is presented in figure 9, Griesemer et al. (insert ref).

If you took a good look at the previous code paragraph, you might have noticed something unexpected. ```struct_lit``` takes a string and a list of expressions in order to construct a new expression. Why is that? In the FG calculus it says that struct literals are composed of a "structure type name" and a list of expressions. What happened to that "structure type name" and what is the string doing there?

For our implementation, field names and field methods will be represented as Makam strings. An FG type, whether it is *ts* (struct type) or *ti* (interface type), or just arbitrary *t*, will be represented also as a string. This seems confusing but will eventually become much clearer. Hang in there reader! Just a few more paragraphs before everything makes sense.

Remember that this is a toy implementation that is interesting for educational and prototyping purposes. So the fact that we represent field names or types with strings is not a serious problem if it simplifies the job.

Sadly Makam does not have type synonyms, [for now](https://github.com/astampoulis/makam/issues/100). So we simply annotate in comments that we will be using strings to represent some of the language constructs.

```
% field = string.
% method = string.
% ts, ti, t = string.
```

As we did with expressions, we can define more language constructs by just translating (almost literally) from the FG calculus.

```
method_sig : type.
method_sig : list string -> string -> method_sig.

method_spec : type.
method_spec : string -> method_sig -> method_spec.

type_lit : type.

struct : list (tuple string string) -> type_lit.
interface : list method_spec -> type_lit.
```

A ```method_sig``` is constructed by passing a list of types (`list string`) and a type (`string`) to its appropriate constructor. We will not be using the method's argument names, we will only be using their types, so to simplify we do not include them in our representation.

A ```method_spec``` is constructed by using a method's name (like "add" or "sort") and it's signature.

Using these ideas, most of the the translation from the calculus to the representation we use is straightforward.

However, one constructor stands out. The ```method_decl``` constructor has this Makam signature:

```
method_decl : string -> method_spec -> (bindone expr (bindmany expr expr)) -> decl.
```

The ```bindone``` and ```bindmany``` look strange at first. In order to construct a ```method_decl```, its constructor needs... (to be continued)

# typecheck.makam

The relationship *<:* is represented by the ```sub``` predicate, meaning subtyping.
The translation between the rules for *<:* in the calculus to the rules for ```sub``` is pretty straightforward.

The *ok* predicate of the calculus is reflected by the ```ok``` predicate in Makam.
The translation necessary for this predicate is also pretty straightforward, except for the rule *T-Func*.

<!-- TODO -->
(explanation missing)

Finally, the predicate *(Γ ⊢ e : t)* is reflected by the Makam predicate ```typecheck```. The main difference being that typecheck has the following signature:

```
typecheck : expr -> string -> prop.
```

Thus, ```typecheck``` is a predicate which relates expressions to strings (indicating types). But where is the context *Γ* (Gamma) ?

<!-- TODO -->
(explanation missing)

Also, notice that we don't need a translation for the *T-Var* rule. This is because we have no representation for contexts and variables. Instead we just use Makam's machinery to check for a variable's type if it is in scope.

# evaluation.makam
