## Reference Solution

The [github repository](https://github.com/confianceai/Challenge-Welding-Reference-Solution-1) contains the code of a naive reference solution proposed for the Welding Quality Detection challenge. This solution is provided as a pedagogical example only and should not be considered a benchmark in terms of performance.

The content of the jupyter notebooks is described as follows:

-   **01-Tutorial.py:** This script demonstrates how to use the main user functions present in this package. It includes examples of how to list available datasets, explore metadata, and draw basic statistics on contextual variables.

-   **02-Create_pytorch_dataloader.py:** This script shows how to use the package to create a PyTorch dataloader.

-   **03-Test_AIComponent.py:** This script demonstrates how to load an AI component and evaluate it by generating operational and uncertainty metrics.

## Starting kit

This [repository](https://github.com/confianceai/Challenge-Welding-Starter-Kit) contains a [template](https://github.com/confianceai/Challenge-Welding-Starter-Kit/tree/main/AI_component_template) to create your own AI component.
You can use it to:
- Complete the myAIComponent class in this [script](https://github.com/confianceai/Challenge-Welding-Starter-Kit/blob/main/AI_component_template/challenge_solution/AIComponent.py)  by filling load_model() and predict() methods which are required so that the evaluation process can interact with your compoent.
- Complete the [setup.py](https://github.com/confianceai/Challenge-Welding-Starter-Kit/blob/main/AI_component_template/setup.py) with the needed information.
- complete the [requirements.txt](https://github.com/confianceai/Challenge-Welding-Starter-Kit/blob/main/AI_component_template/requirements.txt) with your own dependencies.
- Complete the [MANIFEST.in](https://github.com/confianceai/Challenge-Welding-Starter-Kit/blob/main/AI_component_template/MANIFEST.in) with any files you add in the [challenge_solution folder](https://github.com/confianceai/Challenge-Welding-Starter-Kit/tree/main/AI_component_template/challenge_solution) so that your AI component works.

for any issues, write us an email at: challenge.confiance@irt-systemx.fr