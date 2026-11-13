# Group 8 | Synthetic Recruitment Test Data

**50 fictional candidate CVs for our TechCrush AI Automation capstone: From Application to Hire.**

Imagine testing a recruitment system with genuine applicants before its validation, document retrieval, and review stages are ready. One broken link or incorrect routing rule could affect an actual person. Our team instead created 50 synthetic candidate profiles, with varied experience and job relevance, so we could repeatedly test the pipeline without using real applicants.

## Team project and attribution

This dataset supports the **Group 8 AI Recruitment Orchestrator**, a collaborative capstone project. **Grace Omolola Odukoya independently created all 50 synthetic candidate profiles and the accompanying test-data PDFs.** She also served as the Group 8 team lead, coordinated the wider capstone, and implemented the initial application intake workflow. The recruitment system and its modules were built collectively by Group 8 members; this repository is not presented as a solo implementation.

## What's here

- 50 fictional resume PDFs, identified as `CAP26-001` through `CAP26-050`.
- A stable filename pattern: `CAP26-001_Amarachi_Nwankwo.pdf`.
- Synthetic test coverage for profiles with strong, moderate, and weak alignment to the reference role, `JOB-001` (Python Backend Developer).

## How the team used this data

1. Create synthetic profiles and generate readable PDF resumes.
2. Upload each PDF to this public repository, preserving its candidate ID and filename.
3. Construct a direct file URL using the `raw.githubusercontent.com` URL prefix.
4. Submit a JSON payload with a top-level `candidates` array to an **n8n POST webhook**.
5. Validate required fields, download the PDF, extract the text, compare candidate identity, and update Airtable.
6. Examine successful and failed cases before connecting downstream scoring, interview, and approval modules.

### Example payload

```json
{
  "candidates": [
    {
      "candidateId": "CAP26-001",
      "fullName": "Amarachi Nwankwo",
      "email": "capstone.candidate001@example.com",
      "phone": "+234 800 000 0001",
      "jobId": "JOB-001",
      "resumeUrl": "https://raw.githubusercontent.com/graceomolola001-cmyk/group-8-recruitment-test-data/main/CAP26-001_Amarachi_Nwankwo.pdf"
    }
  ]
}
```

For other candidates, replace the ID, name, and PDF filename with a matching fictional profile. Do not reuse one person's CV URL for another profile.

## Replicate the dataset test

1. Clone or download this repository.
2. Open any sample PDF to verify that the file is readable.
3. Use the above JSON payload with your own *test* n8n webhook. Start the test listener before posting.
4. In n8n, use an HTTP Request node configured to download the `resumeUrl` as a file, followed by **Extract From File**.
5. Validate that PDF text and expected candidate name match before writing the structured record to Airtable.
6. Try an invalid `resumeUrl` or missing `jobId` to check error handling.

## Related project documentation

- [Team capstone folder on Google Drive](https://drive.google.com/drive/folders/1SirXxtXzJOiOH5pcO_K0COzGttZO66Ro)
- [Index of 50 synthetic CV links](https://docs.google.com/spreadsheets/d/1ObQ7P_ufyfsfcNcHZRPRd1PN3_LvnkX1czVjppTewpo/edit)
- [Webhook and GitHub setup guide](https://docs.google.com/document/d/1LFTKF5BCJrNYZJv-ZC9gevEeKkg-VBElYUiJeq0KG7w/edit)

## Responsible-use notes

All candidate identities and CV contents are intended to be fictional. Do not upload actual applicants' resumes, personal data, credentials, production webhook URLs, or scoring records here. The dataset supports demonstrations and tests; it does not demonstrate validated live-AI screening or a production-ready recruitment platform.
