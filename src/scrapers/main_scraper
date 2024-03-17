from selenium import webdriver
from selenium.webdriver.support.ui import WebDriverWait
from selenium.webdriver.support import expected_conditions as EC
from selenium.webdriver.common.by import By
from selenium.common.exceptions import NoSuchElementException, TimeoutException
import pandas as pd
import datetime
import logging
import time

def scrape_femicide_data(page_url: str) -> pd.DataFrame:
    log_filename = f'./src/scrapers/logs/anit_sayac_scraper_{datetime.datetime.now().strftime("%Y%m%d%H%M%S")}.log'
    logging.basicConfig(filename=log_filename, level=logging.INFO,
                        format='%(asctime)s - %(levelname)s - %(message)s')

    driver = webdriver.Chrome()
    wait = WebDriverWait(driver, 10)

    try:
        driver.get(page_url)
        logging.info(f"Connected to {page_url}")

        records = []

        try:
            elements = wait.until(EC.visibility_of_all_elements_located((By.XPATH, './/span[contains(@class, "xxy")]')))
            logging.info(f"Scraped all individuals listed in the website. Total: {len(elements)}")
            for individual in elements:
                time.sleep(2)
                anchor = individual.find_element(By.XPATH, './/a[@class="html5lightbox"]')

                name = anchor.text

                href = anchor.get_attribute('href')
                driver_detail = webdriver.Chrome()
                wait = WebDriverWait(driver_detail, 10)
                driver_detail.get(href)
                logging.info(f"Connected to scrape {name} details. RIP...")

                body_text = driver_detail.find_element(By.TAG_NAME, 'body').text
                body_text = body_text.split("\n")

                img_src = driver_detail.find_element(By.TAG_NAME, 'img').get_attribute("src")

                incident_data = {
                    'Name': name,
                    'Tarih': "",
                    'Maktülün yaşı': "",
                    'İl/ilçe': "",
                    'Neden öldürüldü': "",
                    'Kim tarafından öldürüldü': "",
                    'Korunma talebi': "",
                    'Öldürülme şekli': "",
                    'Failin durumu': "",
                    'Kaynak': "",
                    'image': img_src,
                    'url': href
                }

                for line in body_text:
                    if 'Tarih:' in line:
                        incident_data['Tarih'] = line.split(':')[1].strip()
                    elif 'Maktülün yaşı:' in line:
                        incident_data['Maktülün yaşı'] = line.split(':')[1].strip()
                    elif 'İl/ilçe:' in line:
                        incident_data['İl/ilçe'] = line.split(':')[1].strip()
                    elif 'Neden öldürüldü:' in line:
                        incident_data['Neden öldürüldü'] = line.split(':')[1].strip()
                    elif 'Kim tarafından öldürüldü:' in line:
                        incident_data['Kim tarafından öldürüldü'] = line.split(':')[1].strip()
                    elif 'Korunma talebi:' in line:
                        incident_data['Korunma talebi'] = line.split(':')[1].strip()
                    elif 'Öldürülme şekli:' in line:
                        incident_data['Öldürülme şekli'] = line.split(':')[1].strip()
                    elif 'Failin durumu:' in line:
                        incident_data['Failin durumu'] = line.split(':')[1].strip()
                    elif 'Kaynak:' in line:
                        incident_data['Kaynak'] = line.split(':')[1].strip()

                records.append(incident_data)

                driver_detail.quit()
                logging.info(f"Successfully scraped {name} details. RIP...")

                femicide_data = pd.DataFrame(records)
                femicide_data.to_csv("./data/raw/anitsayac_data_all_raw.csv", index=False)

            logging.info("Scraping completed successfully")

        except TimeoutException:
            logging.error("Timeout waiting for elements to be visible")
    except Exception as e:
        logging.error(f"An error occurred: {str(e)}")

    finally:
        driver.quit()

    return femicide_data

scrape_femicide_data("https://anitsayac.com/")
