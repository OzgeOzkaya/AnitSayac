# Anit Sayac Visualization Project

## Overview
This project aims to analyze and visualize data related to femicides in Turkey sourced from [Anıtsayac](https://anitsayac.com), a platform that provides statistics on femicides in the country. Femicide, the killing of women because they are women, is a critical issue globally, and this project seeks to shed light on the situation in Turkey through data analysis and visualization.

## Background
Femicide is a pressing issue worldwide, and Turkey is no exception. Despite efforts to combat gender-based violence, femicides continue to occur at an alarming rate in the country. Anıtsayac serves as a valuable resource for collecting data on these incidents, providing information on victims, perpetrators, locations, and other relevant details.

## Methodology

### Data Collection
Data is scraped from the Anıtsayac website using Python. The following fields are collected for each femicide incident:
- Name
- Year
- Age
- City/Town
- Cause of death
- Perpetrator
- Presence of protection request
- Weapon used
- Status of the murderer
- Source (URL)
- Image (if available)

### Data Processing
The collected data is stored in a dictionary format and then cleaned to ensure consistency and accuracy. Additional trends and insights are explored to enrich the analysis.

### Visualization
The cleaned data is visualized using either Power BI or a basic Django application. Visualizations are created to illustrate the trends and patterns in femicide incidents, highlighting the severity and urgency of the issue.

## Credits
This project is developed by [Your Name]. The data is sourced from [Anıtsayac](https://anitsayac.com), a platform dedicated to tracking femicides in Turkey. Special thanks to the creators of Anıtsayac for providing valuable data for this project.

## Contribution
Contributions to this open-source project are welcome. If you would like to contribute, please follow the guidelines outlined in the project repository.

## License
This project is licensed under the [MIT License](LICENSE). Feel free to use and modify the code for your own purposes.
