# Deployment Checklist

## Pre-deployment

- [x] Move unused files to legacy folder
- [x] Update .gitignore to exclude legacy
- [x] Clean repository structure
- [x] Update README with deployment instructions
- [x] Commit all changes

## Repository Structure

### Production Files:
- `streamlit_app.py` - Main application
- `utils/` - Core functionality modules
- `data_sample/` - Sample data for testing
- `requirements.txt` - Python dependencies
- `README.md` - Deployment instructions

### Documentation:
- `EKSPERIMENTO_ATASKAITA.md` - Experiment report (Lithuanian)
- `VEIKLOS_REZULTATAI.md` - Activity results (Lithuanian)
- `docs/InoBranda verslo planas.docx` - Business plan

### Excluded from deployment (in legacy/):
- Experimental scripts
- Analysis tools
- Raw experiment results
- Intermediate documentation

## Deployment Steps

1. **Clone repository**
   ```bash
   git clone [repository-url]
   cd truck_cargo_matching_v2
   ```

2. **Set up environment**
   ```bash
   python -m venv venv
   source venv/bin/activate  # Windows: venv\Scripts\activate
   pip install -r requirements.txt
   ```

3. **Run application**
   ```bash
   streamlit run streamlit_app.py
   ```

## Verification

- [ ] Application starts without errors
- [ ] Sample data loads correctly
- [ ] Optimization algorithm runs
- [ ] Map visualization displays
- [ ] All UI elements functional

## Production Considerations

1. **Environment Variables**: Configure any production-specific settings
2. **Data Sources**: Update data paths for production data
3. **Performance**: Monitor with larger datasets
4. **Security**: Ensure no sensitive data in repository
5. **Monitoring**: Set up logging and error tracking

## Support

For issues or questions, contact the InoBranda project team.