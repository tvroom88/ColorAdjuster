package contoller;

import static model.PropertyChangeEnabledMutableColor.PROPERTY_GREEN;

import java.awt.Color;
import java.awt.Dimension;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;
import java.awt.event.MouseAdapter;
import java.awt.event.MouseEvent;
import java.awt.event.MouseMotionAdapter;
import java.beans.PropertyChangeEvent;
import java.beans.PropertyChangeListener;
import java.util.Objects;

import javax.swing.BorderFactory;
import javax.swing.ImageIcon;
import javax.swing.JButton;
import javax.swing.JCheckBox;
import javax.swing.JLabel;
import javax.swing.JPanel;
import javax.swing.JSlider;
import javax.swing.JTextField;

import model.ColorModel;
import model.PropertyChangeEnabledMutableColor;

/**
 * Represents a Panel with components used to change and display the Green value for the 
 * backing Color model.
 *
 * @author Charles Bryan
 * @author Your Name
 * @version Autumn 2019
 */
public class GreenRowPanel extends JPanel implements PropertyChangeListener {

    /**  
     * A generated serial version UID for object Serialization. 
     * http://docs.oracle.com/javase/7/docs/api/java/io/Serializable.html
     */
    private static final long serialVersionUID = 2284116355218892348L;
    
    /** The size of the increase/decrease buttons. */
    private static final Dimension BUTTON_SIZE = new Dimension(26, 26);
    
    /** The size of the text label. */
    private static final Dimension LABEL_SIZE = new Dimension(45, 26);
    
    /** The number of columns in width of the TextField. */
    private static final int TEXT_FIELD_COLUMNS = 3;
    
    /** The amount of padding for the change panel. */
    private static final int HORIZONTAL_PADDING = 30;
    
    /** The backing model for the system. */
    private final PropertyChangeEnabledMutableColor myColor;

    /** The CheckBox that enables/disables editing of the TextField. */
    private final JCheckBox myEnableEditButton;
    
    /** The TextField that allows the user to type input for the color value. */
    private final JTextField myValueField;
    
    /** The Button that when clicked increases the color value. */
    private final JButton myIncreaseButton;
    
    /** The Button that when clicked decreases the color value. */
    private final JButton myDecreaseButton;
    
    /** The Slider that when adjusted, changes the color value. */
    private final JSlider myValueSlider;
    
    /** The panel that visually displays ONLY the GREEN value for the color. */
    private final JPanel myColorDisplayPanel;
    
    /**
     * Creates a Panel with components used to change and display the Green value for the 
     * backing Color model. 
     * @param theColor the backing model for the system
     */
    public GreenRowPanel(final PropertyChangeEnabledMutableColor theColor) {
        super();
        myColor = theColor;
        myEnableEditButton = new JCheckBox("Enable edit");
        myValueField = new JTextField();
        myIncreaseButton = new JButton();
        myDecreaseButton = new JButton();
        myValueSlider = new JSlider();
        myColorDisplayPanel = new JPanel();
        layoutComponents();
        addListeners();
    }
    
    /**
     * Setup and add the GUI components for this panel. 
     */
    private void layoutComponents() {
        myColorDisplayPanel.setPreferredSize(BUTTON_SIZE);
        myColorDisplayPanel.setBackground(new Color(0, myColor.getGreen(), 0));
        final JLabel rowLabel = new JLabel("Green: ");
        rowLabel.setPreferredSize(LABEL_SIZE);
        myValueField.setText(String.valueOf(myColor.getGreen()));
        myValueField.setEditable(false);
        myValueField.setColumns(TEXT_FIELD_COLUMNS);
        myValueField.setHorizontalAlignment(JTextField.RIGHT);
        
        final JPanel rightPanel = new JPanel();
        rightPanel.setBorder(BorderFactory.createEmptyBorder(0, 
                                                             HORIZONTAL_PADDING, 
                                                             0, 
                                                             HORIZONTAL_PADDING));
        rightPanel.setBackground(rightPanel.getBackground().darker());
        myIncreaseButton.setIcon(new ImageIcon("./images/ic_increase_value.png"));
        myIncreaseButton.setPreferredSize(BUTTON_SIZE);
        myValueSlider.setMaximum(ColorModel.MAX_VALUE);
        myValueSlider.setMinimum(ColorModel.MIN_VALUE);
        myValueSlider.setValue(myColor.getGreen());
        myValueSlider.setBackground(rightPanel.getBackground());
        myDecreaseButton.setIcon(new ImageIcon("./images/ic_decrease_value.png"));
        myDecreaseButton.setPreferredSize(BUTTON_SIZE);
        myDecreaseButton.setEnabled(false);
        rightPanel.add(myDecreaseButton);
        rightPanel.add(myValueSlider);
        rightPanel.add(myIncreaseButton);
        
        add(myColorDisplayPanel);
        add(rowLabel);
        add(myValueField);
        add(myEnableEditButton);
        add(rightPanel);

    }
    
    /**
     * Add listeners (event handlers) to any GUI components that require handling.  
     */
    private void addListeners() {
        //DO not remove the following statement.
        myColor.addPropertyChangeListener(this);
        
        myIncreaseButton.addActionListener(new IncrementGreenColorComponent());
        myDecreaseButton.addActionListener(new DecrementGreenColorComponent());
        
        myValueSlider.addMouseMotionListener(new ValueSliderComponent1());
        myValueSlider.addMouseListener(new ValueSliderComponent2());
        
        myEnableEditButton.addActionListener(new EnableEditButtonComponent());
               
        myValueField.addActionListener(new ValueFieldComponent1());

    }
    

    @Override
    public void propertyChange(final PropertyChangeEvent theEvent) {
        if (PROPERTY_GREEN.equals(theEvent.getPropertyName())) {
            myValueField.setText(theEvent.getNewValue().toString());
            myValueSlider.setValue((Integer) theEvent.getNewValue());
            myColorDisplayPanel.
                setBackground(new Color(0, (Integer) theEvent.getNewValue(), 0));
        }
        
    }
    // helper functions     
    /**
     * check whether myValueField is number or not.
     * @return true if myValueField is number
     *         false if myValueField is not number
     */
    private boolean isDigit(final String str) {  
        Objects.requireNonNull(str, "the string is empty");
        for(char ch : str.toCharArray()) {    
            if(!Character.isDigit(ch)) return false;
        } 
        return true;
    }
    
    /**
     * according to the number of Blue color, make increase and decrease button enable or not
     */
    private void setIncreDecreButtion() {
        if(myColor.getGreen() >= 255) {
            myIncreaseButton.setEnabled(false);
        }else {
            myIncreaseButton.setEnabled(true);
        }
        
        if(myColor.getGreen() <= 0) {
            myDecreaseButton.setEnabled(false);
        }else {
            myDecreaseButton.setEnabled(true);
        }
    }
    
    /**
     *  if myValueField status is editable and click other component
     *  Get number from myValueField
     */
    private void getTextFieldNumber() {

        if (myValueField.isEditable()) {
            String inStringOfGreen = myValueField.getText().trim();
            if (inStringOfGreen.length() != 0 && isDigit(inStringOfGreen)) {
                int inIntegerOfGreen = Integer.parseInt(inStringOfGreen);
                if (inIntegerOfGreen >= 0 && inIntegerOfGreen <= 255) {
                    myColor.setGreen(inIntegerOfGreen);
                }
            }
        }
        myValueField.setText(String.valueOf(myColor.getGreen()));

    }
 
    //GUI actions
    
    private class IncrementGreenColorComponent implements ActionListener{

        public void actionPerformed(final ActionEvent e) {
            // TODO Auto-generated method stub
            
            getTextFieldNumber();
            
            if(myColor.getGreen() < 255) myColor.adjustGreen(1);
            
            if(myColor.getGreen() >= 255) {
                myIncreaseButton.setEnabled(false);
            }
            if(myColor.getGreen() > 0) {
                myDecreaseButton.setEnabled(true);
            }
        }  
    }
    private class DecrementGreenColorComponent implements ActionListener{

        public void actionPerformed(final ActionEvent e) {
            // TODO Auto-generated method stub
            
            getTextFieldNumber();
            
            if(myColor.getGreen() > 0) myColor.adjustGreen(-1);
            
            if(myColor.getGreen() < 255) {
                myIncreaseButton.setEnabled(true);
            } 
            if(myColor.getGreen() == 0) {
                myDecreaseButton.setEnabled(false);
            }
        }
        
    }
    
    private class EnableEditButtonComponent implements ActionListener{

        public void actionPerformed(final ActionEvent e) {
            // TODO Auto-generated method stub
            getTextFieldNumber();
            if(myEnableEditButton.isSelected()) {
                myValueField.setEditable(true); 
            }else {
                myValueField.setEditable(false);           
            }
            
            setIncreDecreButtion();
        }

    }
    
    private class ValueSliderComponent1 extends MouseMotionAdapter{

        @Override
        public void mouseDragged(final MouseEvent e) {
            // TODO Auto-generated method stub

            myColor.setGreen(myValueSlider.getValue()); 
            setIncreDecreButtion();
        }     
    }
    
    private class ValueSliderComponent2 extends MouseAdapter{
        @Override
        public void mouseClicked(final MouseEvent e) {
            // TODO Auto-generated method stub

            getTextFieldNumber();
            myColor.setGreen(myValueSlider.getValue());
            setIncreDecreButtion();
        }
    }
    
    private class ValueFieldComponent1 implements ActionListener{

        @Override
        public void actionPerformed(final ActionEvent e) {
            // TODO Auto-generated method stub
            getTextFieldNumber();
            setIncreDecreButtion();
        }
    }

}
