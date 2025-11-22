# Research Notes: Math & Code Visualization Tools

## Investigation Log

### November 2025 - Project Initiation

#### Goals
- Systematically investigate math and code visualization tools
- Compare capabilities across different programming languages
- Document best practices for different use cases
- Create practical examples and code samples
- Build comprehensive learning resources

#### Initial Observations

**Key Focus Areas**:
- Mathematical plotting and visualization (Matplotlib, ggplot2, etc.)
- Interactive web-based visualizations (D3.js, Plotly, etc.)
- Algorithm and code execution visualization
- Statistical graphics and data exploration
- Mathematical animations for education

**Market Landscape**:
- Python dominates scientific visualization (Matplotlib ecosystem)
- JavaScript/web tools essential for interactive visualizations
- R remains strong in statistical graphics (ggplot2)
- Julia emerging as high-performance alternative (Makie.jl)
- Specialized tools for specific domains (Manim for math education)

---

## Tool Deep Dives

### Priority 1: Python Core Tools (Immediate Investigation)

#### Matplotlib
- [x] **Status**: Fundamental knowledge established
- **Strengths**:
  - Industry standard, extremely mature
  - Two APIs: pyplot (MATLAB-like) and OOP (object-oriented)
  - Publication-quality output (PDF, SVG, EPS)
  - Extensive customization capabilities
- **Weaknesses**:
  - Verbose for simple plots
  - Not designed for interactivity
  - Steeper learning curve for advanced features
- **Next Steps**:
  - Create comprehensive tutorial series
  - Document pyplot vs OOP approaches
  - Build template library for common plot types
  - Investigate animation capabilities (FuncAnimation)

#### Seaborn
- [ ] **Status**: To investigate
- **Purpose**: Statistical visualization built on Matplotlib
- **Questions**:
  - How much easier is Seaborn vs raw Matplotlib for common statistical plots?
  - What customization is lost vs gained?
  - Best practices for combining Seaborn + Matplotlib?
- **Investigation Plan**:
  - Compare 10 common plots: Seaborn vs Matplotlib code
  - Document style customization options
  - Measure learning curve for beginners

#### Plotly
- [ ] **Status**: To investigate
- **Purpose**: Interactive plotting for web and notebooks
- **Questions**:
  - Performance with large datasets?
  - Offline vs online mode trade-offs?
  - Integration with Dash for dashboards?
- **Investigation Plan**:
  - Build example interactive dashboard
  - Test performance limits
  - Compare with Bokeh for web applications

#### Altair
- [ ] **Status**: To investigate
- **Purpose**: Declarative visualization based on Vega-Lite
- **Questions**:
  - How does declarative approach compare to imperative?
  - Limitations vs flexibility trade-offs?
  - Best use cases?
- **Investigation Plan**:
  - Compare same visualizations in Altair vs Matplotlib
  - Document when declarative approach shines
  - Test customization limits

### Priority 2: Web Visualization (Near-term)

#### D3.js
- [ ] **Status**: To investigate deeply
- **Purpose**: Low-level web visualization library
- **Strengths**:
  - Ultimate flexibility and control
  - Data-driven approach
  - Massive ecosystem and examples
- **Challenges**:
  - Steep learning curve
  - Requires web development knowledge
  - Verbose for simple charts
- **Investigation Plan**:
  - Build 5 fundamental examples (bar, line, scatter, hierarchical, network)
  - Document data binding concepts
  - Compare with higher-level alternatives (Chart.js, Observable Plot)
  - Explore D3 + React integration

#### Observable Plot
- [ ] **Status**: To investigate
- **Purpose**: Modern declarative visualization for Observable notebooks
- **Questions**:
  - How does it compare to D3.js for common tasks?
  - Can it be used outside Observable platform?
  - Migration path from D3.js?

#### Chart.js
- [ ] **Status**: To investigate
- **Purpose**: Simple, easy-to-use charting library
- **Use Case**: Quickly adding charts to web applications

### Priority 3: Specialized Tools

#### Manim
- [ ] **Status**: To investigate
- **Purpose**: Mathematical animations (from 3Blue1Brown)
- **Questions**:
  - Learning curve for non-animators?
  - Render time for complex animations?
  - Best practices for educational content?
- **Investigation Plan**:
  - Create 3-5 example animations
  - Document scene structure and timing
  - Compare Manim Community vs ManimGL

#### Algorithm Visualization Tools
- [ ] Python Tutor - code execution visualization
- [ ] VisuAlgo - algorithm animation platform
- [ ] Custom tools with p5.js or Processing

---

## Comparative Analysis

### Matplotlib vs Seaborn vs Plotly

| Aspect | Matplotlib | Seaborn | Plotly |
|--------|-----------|---------|--------|
| **Use Case** | General plotting, publications | Statistical graphics | Interactive, web, dashboards |
| **Ease of Use** | Moderate | Easy | Moderate |
| **Customization** | Extensive | Moderate (uses Matplotlib) | Extensive |
| **Interactivity** | Limited | None (static) | Excellent |
| **Output Quality** | Publication-quality | Publication-quality | Web-optimized |
| **Learning Curve** | Moderate-High | Low-Moderate | Moderate |
| **Best For** | Scientific papers | Data exploration | Dashboards, presentations |

### Static vs Interactive Visualization

**When to use Static (Matplotlib, Seaborn, ggplot2)**:
- Academic publications and papers
- Printed materials and reports
- Presentations (when interactivity not needed)
- Exploratory data analysis (Jupyter notebooks)
- Vector graphics needed (PDF, SVG)

**When to use Interactive (Plotly, Bokeh, D3.js)**:
- Web applications and dashboards
- Large datasets (filtering/zooming needed)
- User exploration encouraged
- Real-time or streaming data
- Presentations with live demos

---

## Code Examples and Experiments

### Experiment 1: Same Plot, Multiple Libraries

**Goal**: Create identical scatter plot with trend line using 5 different tools

```python
# 1. Matplotlib (pyplot style)
import matplotlib.pyplot as plt
import numpy as np

x = np.random.randn(100)
y = 2*x + np.random.randn(100)*0.5

plt.scatter(x, y, alpha=0.6)
plt.plot(np.linspace(-3, 3, 100), 2*np.linspace(-3, 3, 100), 'r-')
plt.xlabel('X')
plt.ylabel('Y')
plt.title('Scatter Plot with Trend Line')
plt.show()
```

```python
# 2. Matplotlib (OOP style)
fig, ax = plt.subplots(figsize=(8, 6))
ax.scatter(x, y, alpha=0.6)
ax.plot(np.linspace(-3, 3, 100), 2*np.linspace(-3, 3, 100), 'r-')
ax.set_xlabel('X')
ax.set_ylabel('Y')
ax.set_title('Scatter Plot with Trend Line')
plt.show()
```

```python
# 3. Seaborn
import seaborn as sns
import pandas as pd

df = pd.DataFrame({'x': x, 'y': y})
sns.regplot(data=df, x='x', y='y', scatter_kws={'alpha': 0.6})
plt.title('Scatter Plot with Trend Line')
plt.show()
```

```python
# 4. Plotly
import plotly.graph_objects as go
from sklearn.linear_model import LinearRegression

model = LinearRegression()
model.fit(x.reshape(-1, 1), y)
x_line = np.linspace(-3, 3, 100)
y_line = model.predict(x_line.reshape(-1, 1))

fig = go.Figure()
fig.add_trace(go.Scatter(x=x, y=y, mode='markers', marker=dict(opacity=0.6)))
fig.add_trace(go.Scatter(x=x_line, y=y_line, mode='lines', line=dict(color='red')))
fig.update_layout(title='Scatter Plot with Trend Line', xaxis_title='X', yaxis_title='Y')
fig.show()
```

```python
# 5. Altair
import altair as alt

df = pd.DataFrame({'x': x, 'y': y})
chart = alt.Chart(df).mark_circle(opacity=0.6).encode(
    x='x',
    y='y'
) + alt.Chart(df).transform_regression('x', 'y').mark_line(color='red').encode(
    x='x',
    y='y'
)
chart = chart.properties(title='Scatter Plot with Trend Line')
chart.show()
```

**Analysis**:
- Matplotlib OOP: Most verbose, most control
- Seaborn: Shortest code, automatic statistical fitting
- Plotly: Most interactive, slightly more setup
- Altair: Most declarative, composable with `+` operator

### Experiment 2: Mathematical Function Plotting

**Goal**: Plot multiple mathematical functions with LaTeX labels

```python
import matplotlib.pyplot as plt
import numpy as np

x = np.linspace(-2*np.pi, 2*np.pi, 1000)

fig, axes = plt.subplots(2, 3, figsize=(15, 10))
fig.suptitle('Mathematical Functions Gallery', fontsize=16)

# Trigonometric
axes[0, 0].plot(x, np.sin(x), label=r'$\sin(x)$')
axes[0, 0].plot(x, np.cos(x), label=r'$\cos(x)$')
axes[0, 0].plot(x, np.tan(x), label=r'$\tan(x)$')
axes[0, 0].set_ylim(-3, 3)
axes[0, 0].legend()
axes[0, 0].set_title('Trigonometric Functions')
axes[0, 0].grid(True, alpha=0.3)

# Exponential and Logarithmic
x_exp = np.linspace(-3, 3, 100)
axes[0, 1].plot(x_exp, np.exp(x_exp), label=r'$e^x$')
axes[0, 1].plot(x_exp, np.exp(-x_exp), label=r'$e^{-x}$')
axes[0, 1].set_yscale('log')
axes[0, 1].legend()
axes[0, 1].set_title('Exponential Functions')
axes[0, 1].grid(True, alpha=0.3)

# Polynomial
x_poly = np.linspace(-2, 2, 100)
axes[0, 2].plot(x_poly, x_poly**2, label=r'$x^2$')
axes[0, 2].plot(x_poly, x_poly**3, label=r'$x^3$')
axes[0, 2].plot(x_poly, x_poly**4, label=r'$x^4$')
axes[0, 2].legend()
axes[0, 2].set_title('Polynomial Functions')
axes[0, 2].grid(True, alpha=0.3)

# Hyperbolic
axes[1, 0].plot(x, np.sinh(x), label=r'$\sinh(x)$')
axes[1, 0].plot(x, np.cosh(x), label=r'$\cosh(x)$')
axes[1, 0].plot(x, np.tanh(x), label=r'$\tanh(x)$')
axes[1, 0].set_ylim(-5, 5)
axes[1, 0].legend()
axes[1, 0].set_title('Hyperbolic Functions')
axes[1, 0].grid(True, alpha=0.3)

# Bessel Functions
from scipy.special import jv
x_bessel = np.linspace(0, 20, 200)
for n in range(4):
    axes[1, 1].plot(x_bessel, jv(n, x_bessel), label=rf'$J_{n}(x)$')
axes[1, 1].legend()
axes[1, 1].set_title('Bessel Functions')
axes[1, 1].grid(True, alpha=0.3)

# Parametric
t = np.linspace(0, 2*np.pi, 1000)
axes[1, 2].plot(np.sin(3*t), np.cos(4*t))
axes[1, 2].set_aspect('equal')
axes[1, 2].set_title('Lissajous Curve: (sin(3t), cos(4t))')
axes[1, 2].grid(True, alpha=0.3)

plt.tight_layout()
plt.savefig('mathematical_functions_gallery.png', dpi=300, bbox_inches='tight')
plt.show()
```

### Experiment 3: 3D Surface Visualization Comparison

Compare 3D plotting across different libraries:

```python
# Matplotlib 3D
from mpl_toolkits.mplot3d import Axes3D

fig = plt.figure(figsize=(10, 8))
ax = fig.add_subplot(111, projection='3d')

x = y = np.linspace(-5, 5, 50)
X, Y = np.meshgrid(x, y)
Z = np.sin(np.sqrt(X**2 + Y**2))

surf = ax.plot_surface(X, Y, Z, cmap='viridis', alpha=0.8)
ax.set_xlabel('X')
ax.set_ylabel('Y')
ax.set_zlabel('Z')
ax.set_title('3D Surface: $z = \sin(\sqrt{x^2 + y^2})$')
fig.colorbar(surf)
plt.show()
```

```python
# Plotly 3D (much more interactive)
import plotly.graph_objects as go

fig = go.Figure(data=[go.Surface(
    x=X, y=Y, z=Z,
    colorscale='Viridis',
    contours={
        "z": {"show": True, "usecolormap": True, "highlightcolor": "limegreen", "project": {"z": True}}
    }
)])

fig.update_layout(
    title='Interactive 3D Surface',
    scene=dict(
        xaxis_title='X',
        yaxis_title='Y',
        zaxis_title='Z',
        camera=dict(eye=dict(x=1.5, y=1.5, z=1.3))
    ),
    width=900,
    height=700
)

fig.show()
```

---

## Best Practices Discovered

### Matplotlib Best Practices

1. **Choose the Right API**:
   - pyplot (plt.*): Quick exploratory plots, MATLAB users
   - OOP (fig, ax): Production code, multiple subplots, customization

2. **Figure Size and DPI**:
   ```python
   # For screen display
   plt.figure(figsize=(10, 6), dpi=100)

   # For publication
   plt.figure(figsize=(8, 6), dpi=300)
   plt.savefig('figure.png', dpi=300, bbox_inches='tight')
   ```

3. **Color and Style**:
   ```python
   # Use built-in styles
   plt.style.use('seaborn-v0_8-darkgrid')

   # Colorblind-friendly palettes
   import matplotlib.cm as cm
   colors = cm.get_cmap('tab10')  # or 'viridis', 'plasma', etc.
   ```

4. **LaTeX in Labels**:
   ```python
   plt.xlabel(r'$\alpha$')  # Greek letters
   plt.title(r'$f(x) = \frac{1}{\sigma\sqrt{2\pi}} e^{-\frac{(x-\mu)^2}{2\sigma^2}}$')
   ```

5. **Subplots Layout**:
   ```python
   # Uniform grid
   fig, axes = plt.subplots(2, 3, figsize=(15, 10))

   # Custom layout
   fig = plt.figure(figsize=(12, 8))
   ax1 = plt.subplot(2, 2, 1)
   ax2 = plt.subplot(2, 2, 2)
   ax3 = plt.subplot(2, 1, 2)  # Spans both columns
   ```

### Interactive Visualization Best Practices

1. **When to Add Interactivity**:
   - Large datasets requiring zoom/filter
   - Presentations with live demos
   - Web applications
   - Exploratory analysis where users need control

2. **Performance Considerations**:
   - Downsample large datasets for web (WebGL has limits)
   - Use aggregation for millions of points
   - Consider static thumbnails with interactive drill-down

3. **User Experience**:
   - Always include hover tooltips
   - Provide zoom/pan capabilities
   - Add download/export options
   - Clear legends and labels

---

## Open Questions

### Performance
1. **Q**: What is the performance limit for each library with large datasets?
   - **Investigation**: Benchmark 10K, 100K, 1M, 10M points
   - **Tools to test**: Matplotlib, Plotly, Bokeh, VisPy, Datashader

2. **Q**: When should we use GPU acceleration?
   - **Tools**: VisPy (OpenGL), Plotly (WebGL), Makie.jl

### Customization vs Ease of Use
3. **Q**: What's the optimal balance point?
   - **Hypothesis**: Start with high-level (Seaborn), drop to low-level when needed
   - **Test**: Survey developers on customization frequency

### Education
4. **Q**: What's the best learning path for beginners?
   - **Option A**: Start with pyplot, gradually move to OOP
   - **Option B**: Start with Seaborn, learn Matplotlib as needed
   - **Option C**: Start with declarative (Altair), learn imperative later

### Cross-Language Comparison
5. **Q**: How do Python tools compare to R, Julia, MATLAB?
   - **Focus**: ggplot2 vs Matplotlib, Makie.jl vs everything

---

## Next Steps

### Week 1-2: Matplotlib Mastery
- [ ] Complete comprehensive Matplotlib tutorial
- [ ] Document pyplot vs OOP approaches
- [ ] Create template library (20+ common plots)
- [ ] Test animation capabilities
- [ ] Write publication workflow guide

### Week 3-4: Interactive Visualization
- [ ] Build example dashboard with Plotly Dash
- [ ] Create D3.js tutorial for Python developers
- [ ] Compare Bokeh, Plotly, D3.js for same use case
- [ ] Document performance characteristics

### Month 2: Statistical and Scientific
- [ ] Deep dive into Seaborn
- [ ] Explore specialized tools (Mayavi for 3D, VisPy for large data)
- [ ] Document scientific visualization best practices
- [ ] Create examples from real papers

### Month 3: Education and Animation
- [ ] Manim tutorial and examples
- [ ] Algorithm visualization tools survey
- [ ] Create educational content with visualizations
- [ ] Document animation best practices

### Month 4-6: Advanced Topics
- [ ] GPU acceleration comparison
- [ ] Real-time visualization techniques
- [ ] Custom visualization development
- [ ] Integration patterns (web apps, notebooks, reports)

---

## Resources Discovered

### Documentation
- ✅ Matplotlib documentation: Comprehensive, excellent examples
- ✅ Matplotlib gallery: Great for finding examples
- [ ] "Scientific Visualization: Python + Matplotlib" by Nicolas Rougier (book)
- [ ] "Python Data Science Handbook" by Jake VanderPlas

### Tutorials and Courses
- [ ] Real Python Matplotlib guides
- [ ] Matplotlib tutorials (official)
- [ ] Coursera: Data Visualization with Python
- [ ] DataCamp: Interactive visualization tracks

### Communities
- [ ] Matplotlib users mailing list
- [ ] Stack Overflow matplotlib tag
- [ ] r/dataisbeautiful (inspiration)
- [ ] Python Discord #visualization channel

### Code Repositories
- [ ] Matplotlib examples gallery
- [ ] Observable notebooks (D3.js examples)
- [ ] Kaggle visualization kernels
- [ ] GitHub awesome-visualization lists

---

## Ideas and Brainstorming

### Tutorial Series Ideas

1. **"Matplotlib from Zero to Publication"**
   - Part 1: Basics and pyplot
   - Part 2: Object-oriented API
   - Part 3: Subplots and layouts
   - Part 4: Customization and styling
   - Part 5: Publication-quality figures

2. **"Interactive Visualization Cookbook"**
   - Recipe 1: Converting static plots to interactive
   - Recipe 2: Building a dashboard
   - Recipe 3: Real-time data streaming
   - Recipe 4: Large dataset handling

3. **"Mathematical Visualization Guide"**
   - Functions and calculus
   - Linear algebra and transformations
   - Statistics and probability
   - Numerical methods

### Tool Comparison Matrix

Build comprehensive comparison spreadsheets:
- Feature comparison (30+ features)
- Code comparison (10 standard plots)
- Performance benchmarks
- Learning curve assessment
- Use case recommendations

### Example Gallery

Create gallery with:
- 50+ Matplotlib examples
- 20+ Interactive visualizations
- 10+ Mathematical animations
- 10+ Algorithm visualizations
- All with downloadable code

### Best Practices Document

Comprehensive guide covering:
- When to use each tool
- Publication workflow
- Performance optimization
- Accessibility (color, screen readers)
- Reproducibility
- Version control

---

## Meeting Notes and Observations

### 2025-11-22: Project Pivot
- **Original scope**: LLM agent visualization
- **New scope**: Math and code visualization (Matplotlib, etc.)
- **Rationale**: Clarification from stakeholder
- **Impact**: Complete documentation rewrite, but focus is clearer
- **Next**: Deep dive into Python visualization ecosystem

---

## Changelog

### 2025-11-22
- Project scope pivoted to math and code visualization tools
- Rewrote README.md with comprehensive tool survey
- Updated research notes with new focus
- Identified Matplotlib as primary investigation target
- Planned investigation roadmap for next 3-6 months

---

*This is a living document. Update regularly as investigation progresses.*
