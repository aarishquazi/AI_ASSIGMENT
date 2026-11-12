AI REASONING ASSIGNMENT
Student: Aarish Quazi
Roll Number: M26MER008

FILES
-----
reasoning_agent.ipynb
    Use the existing notebook supplied by the student. It contains the
    implementation, public-data evaluation, reasoning tests and CSV exporter.

report.pdf
    Project report describing the representation, algorithms, public
    experiments, reasoning trace and current limitations.

submission.csv
    Public-dataset predictions produced by the reasoning agent. The file
    uses the required columns: id,label. IDs are prefixed by dataset name
    and row position to avoid collisions.

unresolved_public_examples.csv
    Diagnostic list of public examples for which the current agent did not
    return a supported True/False prediction. These cases were not silently
    assigned False and are not included in submission.csv.

ENVIRONMENT
-----------
Recommended: Python 3.10 or newer.

Install the external packages used by the notebook:
    python -m pip install pandas datasets huggingface_hub nltk ipython jupyter

RUNNING THE NOTEBOOK
--------------------
1. Open the existing reasoning_agent.ipynb in Jupyter Notebook or JupyterLab.
2. Restart the kernel and run all cells from top to bottom.
3. The notebook downloads and evaluates these public datasets:
       - RuleTaker: tasksource/ruletaker, dev split (75,872 examples)
       - FOLIO: tasksource/folio, validation split (203 examples)
       - CounterBench: data_balanced_alpha_V1.json (1,000 examples)
         and data_balanced_backdoor_V2.json (200 examples)
4. The public prediction exporter writes submission/submission.csv and
   submission/unresolved_public_examples.csv in the notebook working folder.

CURRENT RECORDED PUBLIC RESULTS
-------------------------------
RuleTaker:
    Total: 75,872; completed: 75,872; coverage: 100.00%.
    Accuracy on completed examples: 100.00%.
    Recorded runtime: approximately 46.293 seconds.

FOLIO:
    Total: 203; completed: 168; coverage: 82.76%.
    Three-class accuracy on completed examples: 83.33%.
    Binary accuracy on completed examples: 91.67%.
    The source labels True, False and Uncertain are mapped to the
    assignment's binary output when a prediction is available; Uncertain
    maps to False for that binary export.
    Recorded runtime: approximately 46.361 seconds.

CounterBench:
    Total: 1,200; completed: 1,190; coverage: 99.17%.
    Accuracy on completed examples: 94.96%.
    Recorded runtime: approximately 0.160 seconds.

PUBLIC CSV STATUS
-----------------
The supplied public submission.csv contains 77,230 resolved predictions:
    RuleTaker:   75,872
    FOLIO:          168
    CounterBench: 1,190
Total public examples: 77,275.
Unresolved examples: 45 (35 FOLIO and 10 CounterBench).
The CSV was checked for the id,label columns, unique IDs, missing values
and labels outside True/False. The 45 unresolved examples are stored in
unresolved_public_examples.csv and are not included in the prediction CSV.
If the course evaluator requires a prediction for every public example,
resolve these cases before considering the public CSV complete.

METHODS AND ASSIGNMENT COMPLIANCE
---------------------------------
The system uses symbolic representations and classical reasoning:
    - RuleTaker: Horn clauses, unification, semi-naive forward chaining,
      stratified negation-as-failure and an alternative backward chainer.
    - FOLIO: first-order formula parsing, quantifier handling, Skolemization,
      CNF conversion, unification, factoring and resolution.
    - CounterBench: structural causal models, abduction, interventions and
      forward simulation.

No generative AI model is used to decide True/False. The final answer is
computed by the symbolic reasoning modules. Routing uses input structure
and content rather than requiring the dataset name as an argument.

PRIVATE EVALUATION
------------------
The private test data was not available and was not used in development.
The notebook includes a separate private-test conversion cell for the TA.
When the evaluator supplies the private file, they can set TEST_FILE (and
TEST_DATASET to 'auto' or the appropriate format) and run the final cell.
The private-test output is separate from the public submission.csv.

IMPORTANT
---------
The report and README were prepared from the existing executed notebook and
supplied public CSV files. The notebook itself has not been changed as part
of preparing these documents. Recorded results are from the saved notebook
run and may vary slightly when rerun on different hardware or package versions.
