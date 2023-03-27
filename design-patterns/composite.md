<div class="markdown prose w-full break-words dark:prose-invert light"><ol><li>Pattern Name: Composite</li></ol><p>The Composite pattern is a structural design pattern that allows you to treat a group of objects as a single object, enabling you to manipulate and manage individual objects and groups of objects in a uniform manner.</p><ol start="2"><li>Problem:</li></ol><p>When designing an application with a hierarchical structure of objects, it can be difficult to manage individual objects and their compositions. The Composite pattern addresses this issue by providing a way to treat both individual objects and groups of objects uniformly.</p><ol start="3"><li>Solution:</li></ol><p>The Composite pattern suggests that you create a class hierarchy that consists of a base component class and its subclasses. The base component defines the interface for all objects in the hierarchy and may also provide some default behavior. Subclasses can be either leaf nodes (individual objects) or composite nodes (groups of objects).</p><ol start="4"><li>Consequences:</li></ol><p>Benefits:</p><ul><li>Simplifies the client code, as it doesn't need to differentiate between individual objects and groups of objects.</li><li>Makes it easier to add new types of components without affecting existing code.</li><li>Promotes code reusability and maintainability.</li></ul><p>Drawbacks:</p><ul><li>Can make the design overly general in some cases, leading to a more complex system.</li></ul><ol start="5"><li>Implementation:</li></ol><p>In Python, you can implement the Composite pattern using abstract base classes and inheritance.</p><ol start="6"><li>Participants:</li></ol><ul><li>Component: An abstract base class defining the common interface for all objects in the hierarchy.</li><li>Leaf: Represents individual objects that don't have children. Inherits from the Component class.</li><li>Composite: Represents groups of objects that can contain other components, including other Composites. Inherits from the Component class.</li></ul><ol start="7"><li>Collaborations:</li></ol><p>Components interact with each other through the interface defined by the Component class. Clients interact with components using the same interface, whether it's a Leaf or a Composite.</p><ol start="8"><li>Real-world example:</li></ol><p>Consider a file system where you have files (individual objects) and directories (groups of objects). Using the Composite pattern, you can treat both files and directories uniformly, making it easier to perform operations such as traversing the file system or calculating the total size.</p><p>Here's a Python implementation of the Composite pattern for the file system example:</p><pre><div class="bg-black rounded-md mb-4"><div class="flex items-center relative text-gray-200 bg-gray-800 px-4 py-2 text-xs font-sans justify-between rounded-t-md"><span>python</span><button class="flex ml-auto gap-2"><svg stroke="currentColor" fill="none" stroke-width="2" viewBox="0 0 24 24" stroke-linecap="round" stroke-linejoin="round" class="h-4 w-4" height="1em" width="1em" xmlns="http://www.w3.org/2000/svg"><path d="M16 4h2a2 2 0 0 1 2 2v14a2 2 0 0 1-2 2H6a2 2 0 0 1-2-2V6a2 2 0 0 1 2-2h2"></path><rect x="8" y="2" width="8" height="4" rx="1" ry="1"></rect></svg>Copy code</button></div><div class="p-4 overflow-y-auto"><code class="!whitespace-pre hljs language-python"><span class="hljs-keyword">from</span> abc <span class="hljs-keyword">import</span> ABC, abstractmethod

<span class="hljs-keyword">class</span> <span class="hljs-title class_">Component</span>(<span class="hljs-title class_ inherited__">ABC</span>):
    <span class="hljs-keyword">def</span> <span class="hljs-title function_">__init__</span>(<span class="hljs-params">self, name</span>):
        self._name = name

<span class="hljs-meta">    @abstractmethod</span>
    <span class="hljs-keyword">def</span> <span class="hljs-title function_">display</span>(<span class="hljs-params">self, indent=<span class="hljs-number">0</span></span>):
        <span class="hljs-keyword">pass</span>

<span class="hljs-keyword">class</span> <span class="hljs-title class_">File</span>(<span class="hljs-title class_ inherited__">Component</span>):
    <span class="hljs-keyword">def</span> <span class="hljs-title function_">display</span>(<span class="hljs-params">self, indent=<span class="hljs-number">0</span></span>):
        <span class="hljs-built_in">print</span>(<span class="hljs-string">f"<span class="hljs-subst">{<span class="hljs-string">' '</span> * indent}</span>- <span class="hljs-subst">{self._name}</span>"</span>)

<span class="hljs-keyword">class</span> <span class="hljs-title class_">Directory</span>(<span class="hljs-title class_ inherited__">Component</span>):
    <span class="hljs-keyword">def</span> <span class="hljs-title function_">__init__</span>(<span class="hljs-params">self, name</span>):
        <span class="hljs-built_in">super</span>().__init__(name)
        self._children = []

    <span class="hljs-keyword">def</span> <span class="hljs-title function_">add</span>(<span class="hljs-params">self, component</span>):
        self._children.append(component)

    <span class="hljs-keyword">def</span> <span class="hljs-title function_">remove</span>(<span class="hljs-params">self, component</span>):
        self._children.remove(component)

    <span class="hljs-keyword">def</span> <span class="hljs-title function_">display</span>(<span class="hljs-params">self, indent=<span class="hljs-number">0</span></span>):
        <span class="hljs-built_in">print</span>(<span class="hljs-string">f"<span class="hljs-subst">{<span class="hljs-string">' '</span> * indent}</span>+ <span class="hljs-subst">{self._name}</span>"</span>)
        <span class="hljs-keyword">for</span> child <span class="hljs-keyword">in</span> self._children:
            child.display(indent + <span class="hljs-number">2</span>)

<span class="hljs-comment"># Client code</span>
root = Directory(<span class="hljs-string">"root"</span>)
documents = Directory(<span class="hljs-string">"documents"</span>)
images = Directory(<span class="hljs-string">"images"</span>)

root.add(documents)
root.add(images)

documents.add(File(<span class="hljs-string">"resume.docx"</span>))
documents.add(File(<span class="hljs-string">"report.pdf"</span>))

images.add(File(<span class="hljs-string">"landscape.jpg"</span>))
images.add(File(<span class="hljs-string">"portrait.png"</span>))

root.display()
</code></div></div></pre><p>This implementation represents files and directories as Leaf and Composite objects, respectively, and allows you to display the file system hierarchy uniformly.</p></div>
