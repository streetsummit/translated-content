---
title: Creating the Hierarchy
slug: orphaned/Web/JavaScript/Guide/The_Employee_Example/Creating_the_Hierarchy
original_slug: Web/JavaScript/Guide/The_Employee_Example/Creating_the_Hierarchy
---
### 階層の作成

Employee の階層を実装するための適当なコンストラクタ関数を定義する方法はいくつかあります。これの定義に何を選択するかは、アプリケーションで何ができるようにしたいかに大きくよります。

このセクションではとても単純（かつ比較的柔軟でない）定義の使用方法を示し、継承を機能させる方法を実際に示します。これらの定義では、オブジェクト作成時に何らかのプロパティの値を指定することはできません。新しく作成されるオブジェクトは単にデフォルトの値を取得するだけです。これは後から変更できます。図 8.2 ではこれらの単純な定義を備えた階層を例示します。

実際のアプリケーションでは、オブジェクト作成時にプロパティの値を設定できるようにするコンストラクタを定義することになるでしょう（詳しくは [より柔軟なコンストラクタ](/ja/Core_JavaScript_1.5_Guide/The_Employee_Example/More_Flexible_Constructors) を参照）。今回はこれらの単純な定義を使用して、継承はどのようにして起こるのかを実際に示していくことにします。

![Image:hier02.gif](/@api/deki/files/1905/=Hier02.gif)
**図 8.2：Employee オブジェクトの定義**

以下に示すように、Java と JavaScript の `Employee` の定義は似ています。唯一の相違点は、Java では各プロパティに対して型を指定する必要があるのに対して、JavaScript ではその必要がないことです。また、Java のクラスでは明示的なコンストラクタメソッドを作成する必要があります。

<table class="fullwidth-table">
  <tbody>
    <tr>
      <th>JavaScript</th>
      <th>Java</th>
    </tr>
    <tr>
      <td>
        <pre>
function Employee () {
this.name = "";
this.dept = "general";
}
</pre
        >
      </td>
      <td>
        <pre>
public class Employee {
   public String name;
   public String dept;
   public Employee () {
      this.name = "";
      this.dept = "general";
   }
}
</pre
        >
      </td>
    </tr>
  </tbody>
</table>

`Manager` および `WorkerBee` の定義では、継承の連鎖において上である次のオブジェクトの指定方法に違いがあります。JavaScript では原型的なインスタンスをコンストラクタ関数の `prototype` プロパティとして追加します。コンストラクタを定義した後ならいつでもそれをすることができます。Java ではクラス定義内でスーパークラスを指定します。クラス定義の外部でスーパークラスを変更することはできません。

<table class="fullwidth-table">
  <tbody>
    <tr>
      <th>JavaScript</th>
      <th>Java</th>
    </tr>
    <tr>
      <td>
        <pre>
function Manager () {
this.reports = [];
}
Manager.prototype = new Employee;

function WorkerBee () {
this.projects = [];
}
WorkerBee.prototype = new Employee;

</pre
        >
      </td>
      <td>
        <pre>
public class Manager extends Employee {
   public Employee[] reports;
   public Manager () {
      this.reports = new Employee[0];
   }
}

public class WorkerBee extends Employee {
public String[] projects;
public WorkerBee () {
this.projects = new String[0];
}
}

</pre
        >
      </td>
    </tr>
  </tbody>
</table>

`Engineer` および `SalesPerson` の定義は、`WorkerBee` の子孫、それゆえに `Employee` の子孫であるオブジェクトを作成します。これらの種類のオブジェクトは連鎖において上にある全オブジェクトのプロパティを持ちます。さらに、これらの定義は `dept` プロパティの継承された値をこれらのオブジェクト固有の新しい値で上書きします。

<table class="fullwidth-table">
  <tbody>
    <tr>
      <th>JavaScript</th>
      <th>Java</th>
    </tr>
    <tr>
      <td>
        <pre>
function SalesPerson () {
   this.dept = "sales";
   this.quota = 100;
}
SalesPerson.prototype = new WorkerBee;

function Engineer () {
this.dept = "engineering";
this.machine = "";
}
Engineer.prototype = new WorkerBee;

</pre
        >
      </td>
      <td>
        <pre>
public class SalesPerson extends WorkerBee {
   public double quota;
   public SalesPerson () {
      this.dept = "sales";
      this.quota = 100.0;
   }
}

public class Engineer extends WorkerBee {
public String machine;
public Engineer () {
this.dept = "engineering";
this.machine = "";
}
}

</pre
        >
      </td>
    </tr>
  </tbody>
</table>

これらの定義を使用して、そのプロパティのデフォルト値を取得するこれらのオブジェクトのインスタンスを作成することができます。図 8.3 ではこれらの JavaScript の定義を使用して新しいオブジェクトを作成する方法を示しています。また、新しいオブジェクトに対するプロパティの値も示しています。

**注意**：*インスタンス*という用語はクラスベース言語においてはある特定の技術的な意味を持っています。これらの言語では、インスタンスとはクラスの個々のメンバであり、クラスとは根本的に異なるものです。JavaScript では「インスタンス」はこの技術的な意味を持っていません。なぜならば JavaScript にはクラスとインスタンスとの間のこの違いがないからです。しかしながら、JavaScript について話す際に、「インスタンス」をある特定のコンストラクタ関数を用いて作成したオブジェクトを意味する言葉として正式ではない形で使用することがあります。例えば、`jane` は `Engineer` のインスタンスであると砕けた言い方をすることもできます。同様に、_親_、_子_、_祖先_、そして*子孫*という用語は JavaScript において正式な意味を持ちませんが、プロトタイプチェーンにおいて上や下にあるオブジェクトについて言及する際にそれらを正式ではない形で使用してもかまいません。

![Image:hier03.gif](/@api/deki/files/1906/=Hier03.gif)
**図 8.3：単純な定義を用いたオブジェクトの作成**

{{ PreviousNext("Core_JavaScript_1.5_Guide:The_Employee_Example", "Core_JavaScript_1.5_Guide:The_Employee_Example:Object_Properties") }}
