# Generic Pivot Subsystem

## GenericPivot.java

'''
package frc.robot.subsystems.GenericPivotSubsystem;

public class GenericPivot extends SubsystemBase {
    private GenericPivotIO io;

    public GenericPivot(GenericPivotIO io) {
        this.io = io;
    }

    @Override
    public void periodic() {
        super.periodic();
        io.periodic();
    }

    public void runSetpoint(Angle angle) {
        io.runSetpoint(angle);
    }

    public Angle getAngle() {
        return io.getAngle();
    }
}
'''

## GenericPivotIO.java

'''
package frc.robot.subsystems.GenericPivotSubsystem;

public interface GenericPivotIO {
    public default void periodic() {}
    public default void runSetpoint(Angle angle) {}
    public default Angle getAngle() { return Degrees.of(0); }
}
'''

## GenericPivotIOTalonFX.java

'''
package frc.robot.subsystems.GenericPivotSubsystem;

public class GenericPivotIOTalonFX implements GroundIntakeIO {
    public static TalonFX pivotTalon = new TalonFX(GenericPivotConstants.pivotTalonID, Constants.canbus);
    public static CANcoder pivotCANcoder = new CANcoder(GenericPivotConstants.pivotCANcoderID, Constants.canbus);

    public static final StatusSignal<Angle> pivotAbsoluteAngle = pivotCANcoder.getAbsolutePosition();
    public static final StatusSignal<Angle> pivotAngle = pivotCANcoder.getPosition();

    public GenericPivotIOTalonFX() {
        TalonFXConfiguration pivotConfig = new TalonFXConfiguration().withCurrentLimits(
            new CurrentLimitsConfigs()
                .withStatorCurrentLimit(GenericPivotConstants.statorCurrentLimit)
                .withSupplyCurrentLimit(GenericPivotConstants.supplyCurrentLimit)
                .withStatorCurrentLimitEnable(true)
                .withSupplyCurrentLimitEnable(true)
        );

        pivotConfig.Feedback.FeedbackRemoteSensorID = pivotCANcoder.getDeviceID();
        pivotConfig.Feedback.FeedbackSensorSource = FeedbackSensorSourceValue.FusedCANcoder;
        pivotConfig.Feedback.SensorToMechanismRatio = GenericPivotConstants.sensorToMechRatio;
        pivotConfig.Feedback.rotorToSensorRatio = GenericPivotConstants.rotorToSensorRatio;
        pivotConfig.MotorOutput.Inverted = InvertedValue.Clockwise_Positive;
        pivotConfig.slot0.GravityType = GravityTypeValue.Arm_Cosine;

        pivotConfig.slot0.kP = GenericPivotConstants.kP;
        pivotConfig.slot0.kI = GenericPivotConstants.kI;
        pivotConfig.slot0.kD = GenericPivotConstants.kD;
        pivotConfig.slot0.kG = GenericPivotConstants.kG;

        pivotConfig.MotionMagic = New MotionMagicConfigs()
            .withMotionMagicAcceleration(GenericPivotConstants.motionMagicAcceleration)
            .withMotionMagicCruiseVelocity(GenericPivotConstants.motionMagicCruiseVelocity);
        
        CANcoderConfiguration canCoderConfig = new CANcoderConfiguration();
        canCoderConfig.MagnetSensor.MagnetOffset = GenericPivotConstants.pivotMagnetOffset;
        canCoderConfig.MagnetSensor.SensorDirection = SensorDirectionValue.Clockwise_Positive;

        pivotTalon.getConfigurator().apply(pivotConfig);
        pivotTalon.setNeutralMode(NeutralModeValue.Brake);
        pivotCANcoder.getConfigurator().apply(canCoderConfig);
    }

    @Override
    public void periodic() {
        BaseStatusSignal.refreshAll(
            pivotAbsoluteAngle,
            pivotAngle
        );
    }

    @Override
    public void runSetpoint(Angle angle) {
        pivotTalon.setControl(new MotionMagicTorqueCurrentFOC(angle.in(Rotations)).withSlot(0));
    }

    @Override
    public Angle getAngle() {
        return Degrees.of(Units.rotationsToDegrees(pivotAngle.getValueAsDouble()));
    }
}
'''

## GenericPivotConstants.java

'''
package frc.robot.subsystems.GenericPivotSubsystem;

public class GenericPivotConstants {
    public static final int pivotTalonID = 0;
    public static final int pivotCANcoderID = 1;

    // Change these values
    public static final Current statorCurrentLimit = Amps.of(55);
    public static final Current supplyCurrentLimit = Amps.of(40);

    public static final double sensorToMechRatio = 1.0/5.0;
    public static final double rotorToSensorRatio = 4.0/3.0;

    public static final double kP = 1;
    public static final double kI = 0;
    public static final double kD = 0.5;
    public static final double kG = 1;

    public static final double motionMagicAcceleration = 24;
    public static final double motionMagicCruiseVelocity = 12;

    public static final double pivotMagnetOffset = 0;
}
'''

## GenericPivotCommands.java

'''
package frc.robot.subsystems.GenericPivotSubsystem;

public class GenericPivotCommands {
    public static Command runSetpoint(GenericPivot pivot, Angle angle) {
        return Commands.runOnce(() -> pivot.runSetpoint(angle));
    }

    public static Command shake(GenericPivot pivot) {
        return Commands.sequence(
            runSetpoint(pivot, Degrees.of(90)),
            Commands.waitUntil(() -> pivot.getAngle().in(Degrees) > 80),
            runSetpoint(pivot, Degrees.of(0))
        );
    }
}
'''
