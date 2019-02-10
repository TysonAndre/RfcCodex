# Annotations

## General idea

Sometimes it is more convenient to write some data that is associated with particular piece of code with that code, rather than in a separate place.

For example, annotations are used to tell the Doctrine ORM how data is stored. For this 'Product' class, the annotation say which database table the data is stored in, the types of the columns and how to  map between 'Products' and 'Projects'.

```

/**
 * @Entity @Table(name="product")
 * A thing that can be paid for
 **/
class Product
{
    /** @Id @Column(type="integer", name="id") @GeneratedValue **/
    protected $id;

    /** @Column(type="string") **/
    protected $name;

    /** @Column(type="string") **/
    protected $description;

    /**
     * @var Project
     * @ManyToOne(targetEntity="Osf\Model\Project")
     * @JoinColumn(name="project_id", referencedColumnName="id")
     */
    protected $project;

    ...

}

```

The problem is, these annotations are string based rather than a defined syntax that is processed by the PHP compiler. The idea would be to make the annotations be part of the code with an appropriate syntax.

```
/**
 * A thing that can be paid for
 **/ 
@Orm\Entity @Orm\Table(name="product")
class Product
{
    @Orm\Id
    @Orm\Column(type="integer", name="id")
    @Orm\GeneratedValue
    protected $id;

    @Orm\Column(type="string")
    protected $name;

    @Orm\Column(type="string")
    protected $description;

    ...

}

```

People would prefer if they were properly defined syntax for various reasons including:

* be able to access them in a standard way across all libraries.
* have syntax checking when they are loaded.
* performance - parsing strings by hand is much slower 


## Hurdles to overcome

### Some people don't like annotations

A lot of people (myself included) don't particuarly like any annotations.

Any RFC for annotations should show clearly how they are better than not having them - e.g. why a parsed version in PHP core is better than the current string versions we have.


### The people who use annotations need to approve of the RFC

The last vote on a RFC that implemented annotations failed on a vote of 14-22.

One of the main reasons for this is that the people who use annotation, particularly Drupal and Doctrine projects said that the proposed implementation 

## Forecast

Will probably happen when some makes an implementation that satisfies the use-cases of the current string based annotations in PHP, and that is technically good enough to be in core.

## Notes

7th time the charm?

https://wiki.php.net/rfc/attributes
https://wiki.php.net/rfc/annotations_v2
https://wiki.php.net/rfc/reflection_doccomment_annotations
https://wiki.php.net/rfc/simple-annotations
https://wiki.php.net/rfc/annotations-in-docblock
https://wiki.php.net/rfc/annotations