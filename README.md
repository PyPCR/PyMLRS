<div align='center'>
    <img src="https://github.com/PyPCR/PyMLRS/blob/main/PyMLRS.png?raw=true", alt="PyMLR Logo">
</div>

<div align="center">
    <br>
        <a href="" width="250px" height="250px" alt="pyHRM"></a>
      <br>
    <h1>PyMLRS</h1>
    <h2><b>A Python library for processing and interpreting DNA High-Resolution Melt and Amplification Curves for the Meningoencephalitis Panel</b></h2>
        <h4>
        <a href="#installing-with-pip">Installation</a>
        •
        <a href="#Features">Features</a>
        •
        <a href="#Documentation">Documentation</a>
        •
        <a href="#getting-help">Help</a>
    </h4>
</div>

# PyMLRS
<p align="justify">
PyMLRS primarily focuses on feature extraction and interpreting results from parsed data. here the first step is to parses files into the .rex format, extracting essential information such as HRM (High Resolution Melting) data, cycle threshold (CT) values, and sample details. It facilitates feature extraction from HRM data by converting it into melt curves, and for parsed CT data, it identifies take-off points crucial for determining the severity of affected pathogens. PyMLRS integrates these features to interpret results and generate comprehensive reports for respective identifiers.<span>
</p>


## Installing with PIP

```
python -m pip install PyMLRS
```
or
```
pip3 install PyMLRS
```

<h1> Classifiers </h1>

<table>
  <tr>
    <td nowrap><strong>Development Status</strong></td><td href = "https://pypi.org/search/?c=Development+Status+%3A%3A+5+-+Production%2FStable"><i >5 - Production/Stable </i></td>
  </tr>
  <tr>
    <td nowrap><strong>Intened Audience</strong></td><td><i>Healthcare</i></td>
  </tr>
  <tr>
    <td nowrap><strong>License</strong></td><td><i>OSI Approved :: MIT License </i></td>
  </tr>
  <tr>
    <td nowrap><strong>Operating System</strong></td><td><i>Microsoft :: Windows :: Windows 10 </i></td>
  </tr>
  <tr>
    <td nowrap><strong>Programming Language</strong></td><td><i>Python 3</i></td>
  </tr>
</table>

## Features
<ol>
  <li>Rextractor
    <ol>
      <li>Extract the data from Rotor Gene Experiment(.rex) files.
        <ol>
          <li>High Resolution Melt (HRM)</li>
          <li>Amplification Curve - Cycle Time (CT)</li>
        </ol>
      </li>
      <li>Processing Data
        <ol>
          <li>Filter Only MEP Pathogens</li>
          <li>Separate by patients</li>
        </ol>
      </li>
    </ol>
  </li>
  <li>MEP panel
    <ol>
      <li>Feature Extraction
        <ol>
          <li>Target – Pathogen Name</li>
          <li>Temperature (Peak of the Melt Curve)</li>
          <li>Width</li>
          <li>Prominence</li>
          <li>Take of Point</li>
          <li>Take down Point</li>
          <li>Area Under the curve</li>
        </ol>
      </li>
      <li>Interactive Visulization.
        <ol>
          <li>High Resolution Melt</li>
          <li>Melt Curve</li>
          <li>Amplification Curve</li>
        </ol>
      </li>
      <li>Result
        <ol>
          <li>Interpreting the results of the pathogens</li>
          <li>Generate report for test Results</li>
        </ol>
      </li>
    </ol>
  </li>
</ol>


<h1> Input Data format </h1>
<p align="justify">
The input file for the library is the run file from the Rotor-Gene machine, which is in the format of a Rotor-Gene Experiment (.rex) file, and we can directly provide the .rex file without any preprocessing.</p>

## Documentation
<html>
<body>
    <h2>Importing Library</h2>
    <pre><code>from PyMLRS.Rextractor import rex_reader
from PyMLRS.Mep_panel import Mep_diagnoser</code></pre>
    <h2>PyMLRS.Rextractor.rex_reader()</h2>
    <pre><code>PyMLRS.Rextractor.rex_reader(path = None)</code></pre>
    <h4>Parameters:</h4>
    <p class="param"><b>path :</b> <i>Rotor Gene Experiment file path (.rex)</i></p>
    <h4>Returns:</h4>
    <p class="param"><b>A dictionary containing various patient ID for each separate patients:</b> <i>class 'dict_keys'</i></p>
    <p class="param"><b>A dictionary containing various dataframes (HRM) for respective patient ID's:</b> <i>class 'dict_keys'</i></p>
    <p class="param"><b>A dictionary containing various dataframes (CT) for respective patient ID's:</b> <i>class 'dict_keys'</i></p>
</body>
</html>

<br>

### Example
```
from PyMLRS.Rextractor import rex_reader
Patient_ids,raw_hrm,raw_ct = rex_reader("your .rex file path")
```
## PyMLRS.Mep_panel.Mep_diagnoser 
```
md = Mep_diagnoser()

hrm_data = md.transform_hrm(dataframe: Any,figure: bool = False)
ct_data = md.transform_ct(dataframe: Any,figure: bool = False)
melt = md.hrm_to_melt(figure: bool = False)
hrm_features = md.hrm_feature_extraction()
ct_values = md.ct_value()
md.Tm_threshold()
result = md.predict_result()
report = md.report( output_fie_path: Any,patient_id: Any)
```

<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
</head>
<body>
<h2>Function Documentation</h2>

<h2><code>transform_hrm</code></h2>

<p><strong>Parameters:</strong></p>
<ul>
  <li><code>dataframe</code>: HRM data obtained from <code>rex_reader()</code>.</li>
  <li><code>figure</code> (optional): Boolean flag indicating whether to generate an HRM graph.</li>
</ul>

<p><strong>Returns:</strong></p>
<ul>
  <li>Processed HRM data.</li>
  <li>If <code>figure</code> is <code>True</code>, an HRM graph is also returned.</li>
</ul>

<h2><code>transform_ct</code></h2>

<p><strong>Parameters:</strong></p>
<ul>
  <li><code>dataframe</code>: CT data acquired from <code>rex_reader()</code>.</li>
  <li><code>figure</code> (optional): Boolean flag to specify if a CT graph should be produced.</li>
</ul>

<p><strong>Returns:</strong></p>
<ul>
  <li>Processed CT data.</li>
  <li>If <code>figure</code> is <code>True</code>, a CT graph is included in the output.</li>
</ul>

<h2><code>hrm_to_melt</code></h2>

<p><strong>Parameters:</strong></p>
<ul>
  <li><code>figure</code> (optional): Boolean flag for generating a melt graph.</li>
</ul>

<p><strong>Returns:</strong></p>
<ul>
  <li>Melted data.</li>
  <li>If <code>figure</code> is <code>True</code>, a melt graph is also provided.</li>
</ul>

<h2><code>hrm_feature_extraction</code></h2>

<p><strong>No Parameters Needed</strong></p>

<p><strong>Returns:</strong></p>
<ul>
  <li>HRM features extracted from the data.</li>
</ul>

<h2><code>ct_value</code></h2>

<p><strong>No Parameters Needed</strong></p>

<p><strong>Returns:</strong></p>
<ul>
  <li>CT values derived from the data.</li>
</ul>

<h2><code>predict_result</code></h2>

<p><strong>No Parameters Needed</strong></p>

<p><strong>Returns:</strong></p>
<ul>
  <li>Predicted result based on the processed data.</li>
</ul>

<h2><code>report</code></h2>

<p><strong>Parameters:</strong></p>
<ul>
  <li><code>output_file_path</code>: Path to save the generated report.</li>
  <li><code>patient_id</code>: Identifier for the patient.</li>
</ul>

<p><strong>Returns:</strong></p>
<ul>
  <li>Generated report based on the analysis.</li>
</ul>

</body>
</html>


### Sample code Snippet for interpreting individual result 
```
from PyMLRS.Rextractor import rex_reader
from PyMLRS.Mep_panel import Mep_diagnoser

# File extraction from the rex file
patient_id,hrm,ct = rex_reader("Your .rex file path")
print(patient_id)
```

```
# Create Object
md = Mep_diagnoser()

# Interpreting the results by providing patient ID manually
hrm_data = md.transform_hrm(hrm[id])
ct_data = md.transform_ct(ct[id])
melt = md.hrm_to_melt(figure = False)
hrm_features = md.hrm_feature_extraction()
ct_values = md.ct_value()
result = md.predict_result()
report = md.report( output_fie_path=f"{id}.pdf",patient_id=id)

```

### Sample code Snippet for interpreting all individual result 
```
from PyMLRS.Rextractor import rex_reader
from PyMLRS.Mep_panel import Mep_diagnoser

# File extraction from the rex file
patient_id,hrm,ct = rex_reader("Your .rex file path")

# Interpreting the results
for id in patient_id:
    md = Mep_diagnoser()
    hrm_data = md.transform_hrm(hrm[id])
    ct_data = md.transform_ct(ct[id])
    melt = md.hrm_to_melt(figure = False)
    hrm_features = md.hrm_feature_extraction()
    ct_values = md.ct_value()
    result = md.predict_result()
    report = md.report( output_fie_path=f"{id}.pdf",patient_id=id)
```

# Getting Help

If you need to get in touch with the team, please contact through email address:<br>
[chandruganeshan24@gmail.com](mailto:chandruganeshan24@gmail.com)<br>
[vikramsekar2305@gmail.com](mailto:vikramsekar2305@gmail.com) 

# Developers
The developer of this Software are M.Sc Data Analytics Students in Department of Computer Application at [Bharathiar University](https://b-u.ac.in/23/department-computer-applications)
<table style='width:40%'>
  <tbody>
    <tr>
      <td align='center' valign='top'><a href="https://github.com/chandru-g24"> <img src="https://avatars.githubusercontent.com/u/111188572?s=400&u=befb7d97d2b8419a715a22b09d92f825bdc33906&v=4" width = '60px;' alt='Chandru G'/> <br /> <sub><b><a href="https://www.linkedin.com/in/chandru-g24/"> Chandru Ganeshan</a></b></sub></a><br /></td>
      <td align='center' valign='top'><a href="https://github.com/Vikram2305"> <img src="https://avatars.githubusercontent.com/u/124907782?s=400&u=a5d9c4ca9f08e5bb5e88bc4d049d5e80703d1c89&v=4" width = '60px;' alt='Vikram S'/> <br /> <sub><b><a href="https://www.linkedin.com/in/vikram-sekar/"> Vikram Sekar</a></b></sub></a><br /></td>
    </tr>
  </tbody>
  
</table>
