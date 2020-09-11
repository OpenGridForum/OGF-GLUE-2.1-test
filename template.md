# 5. Template

In order to enrich the UML Class Diagrams with additional information, a table for each UML class is provided. This descriptive table is composed of three parts.

The ﬁrst part refers to the whole entity and presents the entity name, the entity from which it inherits and the description of what the entity represents.

The second part refers to the properties of the class; for each of them, the following characteristics are described: the attribute name, the data type, the multiplicity concerning how many values are allowed \(\* means zero or more\), the unit of measurement and a description. For ease of reading, the properties that are inherited from a parent class are also listed. As regards the multiplicity, the value of zero means that it is allowed to refrain from publishing a value for the related attribute even though this MAY be measured.

The third part refers to the associations \(association, composition, aggregation or association class\) that the class MAY hold with other classes. For each association, the associated class reference is described in terms of the associated end class and key attribute, the multiplicity \(i.e., the number of instances of the associated class that are allowed\) and a description. The inherited associations are also reported in the “inherited association end” if they are not redefined in the “association end”. The template structure is the following:

| Entity | Inherits from | Description |  |  |
| :--- | :--- | :--- | :--- | :--- |
|  |  |  |  |  |
| Inherited Attribute | Type | Mult. | Unit | Description |
|  |  |  |  |  |
| Attribute | Type | Mult. | Unit | Description |
|  |  |  |  |  |
| Association End | Mult. | Description |  |  |
|  |  |  |  |  |
| Inherited Association End | Mult. | Description |  |  |
|  |  |  |  |  |

